<template>
  <div class="post-list">
    <div v-for="post in posts" :key="post.id" class="post">
      <div class="type">{{ post.postType }}</div>
      <img :src="post.featured_image" alt="Featured Image" />
      <div class="minRead">{{ post.formattedDate }} - {{ post.avgMinuteRead }} min read</div>
      <a :href="post.permalink"
        ><h2 class="post-title">{{ post.title ? post.title.rendered : "" }}</h2></a
      >
      <div class="post-content" v-html="post.content ? post.content.rendered : ''"></div>
      <div class="row-cta">
        <button class="cta">How to do this</button>
        <button class="cta">HR Stuff</button>
      </div>
    </div>
  </div>
  <button class="cta load" @click="loadMore">Load more</button>
</template>

<script>
import axios from "axios";

const url = import.meta.env.VITE_API_URL;

const calculateReadingTime = (content) => {
  const wordCount = content.trim().split(/\s+/).length;
  const imageCount = content.split("<img").length - 1;
  const textTime = Math.ceil(wordCount / 200);
  const imageTime = (imageCount * 10) / 60;
  return Math.round(textTime + imageTime);
};

const formatPost = (post) => {
  const { id, title, link, date, content, _embedded } = post;
  const formattedDate = new Date(date).toLocaleDateString("en-US", {
    month: "short",
    day: "numeric",
    year: "numeric",
  });
  const avgMinuteRead = calculateReadingTime(content.rendered);
  const postType = _embedded["wp:term"][0][0].name;
  const featured_image = _embedded["wp:featuredmedia"][0]?.source_url || "";
  return { id, title, permalink: link, formattedDate, avgMinuteRead, postType, content, featured_image };
};

export default {
  data() {
    return {
      posts: [],
      page: 1,
    };
  },
  mounted() {
    this.fetchPosts(1);
  },
  methods: {
    fetchPosts(page) {
      axios
        .get(`${url}/wp-json/wp/v2/posts?_embed&page=${page}&per_page=9`)
        .then((response) => {
          this.posts = response.data.map(formatPost);
        })
        .catch((error) => {
          console.error(error);
        });
    },

    loadMore() {
      axios
        .get(`${url}/wp-json/wp/v2/posts?_embed&page=${this.page + 1}`)
        .then((response) => {
          const newPosts = response.data.map(formatPost);
          this.posts.push(...newPosts);
          this.page += 1;
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
};
</script>

<style>
.post-list {
  width: min(80%, 1140px);
  margin: 81px auto;

  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 65px 42px;
}

.post {
  position: relative;
  display: grid;
  gap: 15px;
}

.post .type {
  position: absolute;
  z-index: 1;
  top: 18px;
  left: 22px;
  font-size: 14px;
  padding: 4px 8px;
  border-radius: 5px;
  color: #fff;
  background-color: var(--clr-tertiary);
}

.post img {
  width: 100%;
  height: 256px;
  object-fit: cover;
}

.post-content p {
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 3; /* Number of lines to show */
  -webkit-box-orient: vertical;
}

.minRead {
  color: var(--clr-400);
  font-family: "Sofia Pro SemiBold", sans-serif;
}

a:has(.post-title) {
  color: inherit;
  text-decoration: none;
  font-family: "Sofia Pro Bold", sans-serif;
}

.row-cta {
  display: flex;
  gap: 18px;
}

.cta {
  color: var(--clr-accent);
  border: 1px solid var(--clr-accent);
  border-radius: 8px;
  background-color: transparent;
  padding: 4px 8px;
  cursor: pointer;
}

.cta.load {
  font-family: "Sofia Pro SemiBold", sans-serif;
  padding: 11px 30px;
  margin-inline: auto;
  display: block;
}
</style>
