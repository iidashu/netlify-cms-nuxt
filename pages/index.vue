<template>
  <div class="container">
    <div v-for="post in posts" :key="post.slug">
      <div class="post">
        <h1>{{ post.title }}</h1>
        <nuxt-content :document="post" />
      </div>
      <hr />
    </div>
  </div>
</template>

<script>
export default {
  head() {
    return {
      script: [
        { src: "https://identity.netlify.com/v1/netlify-identity-widget.js" },
      ],
    };
  },
  async asyncData({ $content, params, error }) {
    let posts;
    try {
      posts = await $content("blog", params.slug).fetch();
      // OR const article = await $content(`articles/${params.slug}`).fetch()
    } catch (e) {
      error({ message: "Blog Post not found" });
    }

    return {
      posts,
    };
  },
};
</script>

<style>
.container {
  margin: 0 auto;
  padding: 80px;
  /* min-height: 100vh; */
  /* display: flex;
  justify-content: center;
  align-items: center;
  text-align: center; */
}

/* .title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
} */

.post {
  text-align: left;
}

hr {
  margin: 80px 0;
}
</style>
