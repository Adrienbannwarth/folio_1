<template>
  <Layout>
    <g-link class="link__back" to="/">Home</g-link>
    <!-- <div v-bind:style="{ ['height']: 'calc(' + scrollbar() + '% - 150px)' }" class="scrollbar"></div> -->
    <div id="top" class="container">
      <h1 class="about__title">About</h1>
      <p class="about__desc">{{$page.about.description}}</p>

      <p class="about__subtitle">What i usually do</p>
      <p class="about__details">
        <span href>Dev front</span>
        <span href>Design</span>
      </p>
      <p class="about__subtitle">Contact & social</p>
      <p class="about__details">
        <a href>Dribble</a>
        <a href>Linkedin</a>
      </p>
      <div class="about__footer">
        <p class="about__subtitle">
          Dev by
          <a class="about__link" href="https://adrienbannwarth.com" target="_blank">Adrien</a>
        </p>
        <a class="about__link" href="#top">Back to top</a>
      </div>
    </div>
  </Layout>
</template>
<page-query>
query {
  about: allAbout {
      description
  }
}
</page-query>
<script>
import { TweenMax, Back, gsap, Expo } from "gsap";
export default {
  metaInfo: {
    title: "About us"
  },
  data() {
    return {
      scrolled: 100
    };
  },
  methods: {
    scrollbar() {
      var winScroll =
        document.body.scrollTop || document.documentElement.scrollTop;
      var height =
        document.documentElement.scrollHeight -
        document.documentElement.clientHeight;
      this.scrolled = (winScroll / height) * 100;
      return this.scrolled;
    }
  },
  mounted() {
    window.addEventListener("scroll", this.scrollbar);
    console.log(this.scrollbar);
  }
};
</script>