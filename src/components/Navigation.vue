<template lang="pug">
	nav(:class="{navBg:biographyFlag}").nav
		div.nav__h1
			h1.nav__h1--headline
				router-link(:to="{name:'Home'}",target="page").nav__link--txt Philosophia
			News(v-if="biographyFlag")
		ul(v-if="biographyFlag").nav__year
			li(v-for="(year,i) in yearList",:key="i",@click="yearClick(i)") {{year}}
</template>

<script>
import News from "@/components/News.vue";
import Mixin from "@/mixins/Mixin.vue";
export default {
  name: "Navigation",
  props: ["biographyFlag"],
  data() {
    return {
      yearList: ["2021", "2020", "2019", "2018"],
    };
  },
  components: {
    News,
  },
  mixins: [Mixin],
  methods: {
    yearClick(i) {
      this.$emit("yearClickData", this.yearList[i]);
    },
  },
};
</script>

<style lang="scss">
@import "@/assets/scss/common.scss";
nav {
  position: fixed;
  top: 0;
  z-index: 25;
  a {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100%;
    transition: 0.2s color, 0.2s background;
  }
}
.navBg {
  background: rgba($color: $baceColor, $alpha: 0.8);
}
@media screen and (min-width: 481px) {
  /* PCサイト */
  .nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100vw;
    height: 160px;
    padding: 0 5vw;
    color: $accentColor;
    &__h1 {
      display: flex;
      justify-content: flex-start;
      align-items: center;
      height: 100%;
      &--headline {
        font-size: 3rem;
        font-family: $font;
        margin-right: 16px;
      }
    }
    &__year {
      display: flex;
      justify-content: flex-start;
      align-items: center;
      font-size: 2rem;
      font-family: $font2;
      margin-right: 15vw;
      li {
        display: flex;
        justify-content: center;
        align-items: center;
        width: 80px;
        height: 32px;
        margin-left: 8px;
        position: relative;
        &::after {
          content: "";
          display: block;
          width: 100%;
          height: 100%;
          background: transparent;
          position: absolute;
          top: 0;
          left: 0;
          transition: 0.2s background;
        }
        &:hover {
          &::after {
            background: #fdbbbb;
          }
        }
      }
    }
  }
}
@media screen and (max-width: 480px) {
  /* スマホサイト */
  nav {
    // background: rgba(238, 238, 238, 0.8);
    height: 50px;
    right: 0;
    z-index: 25;
    width: 100vw;
    ul {
      display: flex;
      justify-content: flex-start;
      padding-left: 15px;
      li {
        a {
          color: $accentColor;
        }
        &:last-child {
          display: none;
        }
      }
    }
    .nav__link--txt {
      a {
        padding: 0 10px;
        span {
          display: inline-block;
        }
        &:hover {
          color: darken($accentColor, 20%);
        }
      }
    }
  }
}
</style>
