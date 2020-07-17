<template>
  <div class="footer">
    <div @click="menuOpen" class="footer__projects">
      <g-link class="projects__link" to="/">All projects</g-link>
      <div class="btn__project">
        <div class="point__content">
          <i class="point"></i>
          <i class="point"></i>
          <i class="point"></i>
          <i class="point"></i>
          <i class="point"></i>
          <i class="point"></i>
          <i class="point"></i>
          <i class="point"></i>
          <i class="point"></i>
        </div>
      </div>
    </div>

    <div :class="MenuIsOpen == true ? 'isOpen' : ''" class="menu__content">
      <a class="btn__close" @click="MenuIsOpen = !MenuIsOpen" href>close</a>
      <nav class="menu">
        <div v-for="(article, index) in $page.articles.edges" :key="article.id" class="menu__item">
          <span class="menu__index">{{index +1}}</span>
          <a class="menu__item-link">{{article.node.title}}</a>
          <img class="menu__item-img" :src="''+ article.node.image +''" alt="Some image" />
          <div class="marquee">
            <div class="marquee__inner" aria-hidden="true">
              <span>{{article.node.title}}</span>
              <span>{{article.node.title}}</span>
              <span>{{article.node.title}}</span>
              <span>{{article.node.title}}</span>
            </div>
          </div>
        </div>
      </nav>
    </div>
  </div>
</template>

<script>
import { TweenMax, Back, gsap, Expo } from "gsap";
export default {
  metaInfo: {
    title: "footer"
  },
  data() {
    return {
      MenuIsOpen: false
    };
  },
  methods: {
    menuOpen() {
      this.MenuIsOpen = !this.MenuIsOpen;

      TweenMax.from(".menu__item", 1, {
        y: 50,
        opacity: 0,
        delay: 0.2,
        ease: Back.easeInOut
      });
      TweenMax.from(".btn__close", 1.5, {
        x: -30,
        opacity: 0,
        delay: 0.3,
        ease: Back.easeInOut
      });
    }
  }
};
</script>
