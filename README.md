# App Name

## Introduction

This app is a Vue.js and WordPress app that allows users to view and load blog posts from a WordPress site.

## Features

- Displays blog posts with titles, featured images, post types, and estimated reading times.
- Supports loading more posts with a "Load More" button.
- Displays formatted dates in "MMM dd, yyyy" format.

## Requirements

- Node.js and npm installed on your local machine.
- A WordPress site with the WP REST API plugin installed and enabled.

## Installation

1. Clone the repository to your local machine.
2. Navigate to the project directory and run the following command in the terminal:

```js
npm install
```

3. Create a new file called .env.local in the project directory and add the following line, replacing YOUR_WORDPRESS_URL with the URL of your WordPress site:

```js
VUE_APP_API_URL = YOUR_WORDPRESS_URL;
```

## Usage

1. To start the app, run the following command in the terminal:

```js
npm run serve
```

2. The app will be available at http://localhost:8080.
3. On the home page, you will see the most recent 9 blog posts from your WordPress site.
4. Clicking on a blog post title will take you to the full blog post on your WordPress site.
5. To load more posts, click the "Load More" button at the bottom of the page.
6. The estimated reading time for each post is displayed beneath the post title, in minutes.
7. The formatted date for each post is displayed in "MMM dd, yyyy" format, beneath the post type.

## Troubleshooting

If you encounter any issues while using this app, please check the following:

- Ensure that your WordPress site has the WP REST API plugin installed and enabled.
- Check that the VUE_APP_API_URL environment variable in your .env.local file is set correctly to the URL of your WordPress site.
- Check the browser console for any error messages.

## Conclusion

This app provides a simple and easy-to-use way for users to view and load blog posts from a WordPress site. With its clear and concise interface and helpful features, it's a great tool for anyone looking to access blog content from their WordPress site.

## Example

Here is the link for the deployed Vue.js project: https://coricsdev.github.io/vue-project/. Additionally, you can find the link where the Vue.js application is fetching WordPress posts at: https://sandbox-one.dadizrico.com/.
