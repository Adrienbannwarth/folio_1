<template>
  <Layout>
    <div class="articlePage">
      <div
        class="articlePage__img"
        :style="{ 'background-image': 'url(' + $page.article.image + ')' }"
      ></div>
      <div class="container">
        <g-link to="/" class="back">Back</g-link>
        <h1 class="articlePage__title">{{$page.article.title}}</h1>
        <p>{{$page.article.author}}</p>
        <p>{{$page.article.date}}</p>
        <div v-html="$page.article.content"></div>
      </div>
    </div>
  </Layout>
</template>
<page-query>
query ($path: String!) {
  article: articles (path: $path) {
    title
    content
    author
    image
  }
}
</page-query>
<script>
export default {
  components: {},
  metaInfo() {
    return {
      title: this.$page.article.title
    };
  }
};
</script>
<style>

.articlePage__img {
  width: 100%;
  height: 400px;
  background-size: cover;
  background-position: center;
}
.back {
  display: flex;
  align-items: center;
  color: #333;
  text-decoration: none;
}
</style>