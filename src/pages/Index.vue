<template>
  <Layout>
    <Header />
    <div class="swiper-container">
      <div class="swiper-wrapper">
        <div
          v-for="(article, index) in $page.articles.edges"
          :key="article.id"
          class="project__container swiper-slide"
        >
          <div class="project__content">
            <div class="project__body">
              <p class="project__index">
                {{index + 1}}
                <span class="project__index__total">/ {{$page.articles.edges.length}}</span>
              </p>
              <div class="project__title">
                <div class="project__content__link">
                  <g-link :to="article.node.path" class="project__link">{{article.node.title}}</g-link>
                </div>
                <div class="marquee">
                  <div class="marquee__inner">
                    <span>{{article.node.title}}</span>
                    <span>{{article.node.title}}</span>
                    <span>{{article.node.title}}</span>
                    <span>{{article.node.title}}</span>
                  </div>
                </div>
              </div>
              <p class="project__subtitle">{{article.node.subtitle}}</p>
            </div>
            <div
              class="project__img"
              :style="{ 'background-image': 'url(' + article.node.image + ')' }"
            ></div>
          </div>
        </div>
      </div>
      <div class="scroll__content">
        <span class="scroll__text">Scroll</span>
        <span class="scroll__subtitle">Down</span>
      </div>
      <!-- If we need navigation buttons -->
      <!-- <div class="swiper-button-prev"></div>
      <div class="swiper-button-next"></div>-->
    </div>
    <Footer />
  </Layout>
</template>
<page-query>
query {
  articles: allArticles {
    edges {
      node {
        title
        abstract
        subtitle
        image
        path
      }
    }
  }
}
</page-query>
<script>
// import Swiper JS
import Swiper, { Navigation, Pagination, Mousewheel } from "swiper";
Swiper.use([Navigation, Pagination, Mousewheel]);
// import Swiper styles
import "swiper/swiper-bundle.css";

import { TweenMax, Back, gsap, Expo } from "gsap";

import Header from "../components/Header";
import Footer from "../components/Footer";

export default {
  components: {
    Header,
    Footer
  },
  metaInfo: {
    title: "My blog"
  },
  data() {
    return {

    };
  },

  mounted() {
    var mySwiper = new Swiper(".swiper-container", {
      direction: "horizontal",
      // loop: true,
      mousewheel: true,
      speed: 700,
      pagination: {
        el: ".swiper-pagination"
      },
      navigation: {
        nextEl: ".swiper-button-next",
        prevEl: ".swiper-button-prev"
      },
      scrollbar: {
        el: ".swiper-scrollbar"
      }
    });
    TweenMax.from(".project__content__link", 1, {
      y: 30,
      opacity: 0,
      delay: 0.1,
      ease: Back.easeInOut
    });
    TweenMax.from(
      ".project__subtitle",
      1,
      {
        y: 30,
        opacity: 0,
        delay: 0.2,
        ease: Back.easeInOut
      },
      "-=2"
    );
    // TweenMax.from(
    //   ".project__img",
    //   1,
    //   {
    //     y: 30,
    //     scale: 0.9,
    //     delay: 0.2,
    //     ease: Back.easeInOut
    //   },
    //   "-=2"
    // );

    mySwiper.on("slideChange", function() {
      console.log("CHANGED");
      TweenMax.from(".project__content__link", 1, {
        y: 30,
        opacity: 0,
        delay: 0.1,
        ease: Back.easeInOut
      });
      TweenMax.from(
        ".project__subtitle",
        1,
        {
          y: 30,
          opacity: 0,
          delay: 0.2,
          ease: Back.easeInOut
        },
        "-=2"
      );
    });
  },

  methods: {}
};
</script>