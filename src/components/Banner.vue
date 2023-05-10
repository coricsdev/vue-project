<template>
  <div class="banner">
    <h1 class="title">{{ title }}</h1>
    <p>{{ description }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "Insights & Resources",
      description: "Introductory copy that goes underneath the H1 to better contextualise what this does and who it’s for.",
    };
  },
};
</script>

<style>
.banner {
  background: var(--clr-700);
  background-image: linear-gradient(156deg, var(--clr-700) 0%, var(--clr-400) 100%);
  color: #fff;

  display: grid;
  grid-template-columns: min(40%, 1440px);

  padding: 110px 150px 115px;
}
.title {
  padding-bottom: 31px;
}
</style>
