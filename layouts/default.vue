<template>
  <div class="main">
    <div class="sidebar">
      <NuxtLink class="logo-link" to="/">
        <img class="logo-small" src="@/assets/icon.min.svg" alt="ViewTube" />
        <h1 class="logo">
          <span>View</span>
          <span class="logo-colored">Tube</span>
          <div class="wiki-text-clip">
            <span class="wiki-text">.wiki</span>
          </div>
        </h1>
      </NuxtLink>
      <div v-if="pageLinks" class="pages-list">
        <NuxtLink
          v-for="page in pageLinks"
          :key="page.slug"
          class="page-link"
          :to="`/${page.slug}`"
          >{{ page.title }}</NuxtLink
        >
      </div>
    </div>
    <Nuxt />
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  data() {
    return {
      pageLinks: [] as any
    }
  },
  async fetch() {
    this.pageLinks = await this.$content().fetch()
  }
})
</script>

<style lang="scss">
html,
body {
  margin: 0;
  background-color: $bgcolor-main;
  font-family: sans-serif;
  color: $title-color;
}

.main {
  display: flex;
  flex-direction: row;

  @media screen and (max-width: 700px) {
    flex-direction: column;
  }

  .sidebar {
    position: sticky;
    top: 0;
    width: $sidebar-width;
    height: 100%;
    display: flex;
    flex-direction: column;
    z-index: 800;
    box-shadow: 0;

    @media screen and (max-width: 700px) {
      background-color: $bgcolor-main;
      width: 100%;
    }

    .logo-link {
      font-family: $header-font;
      padding: 20px;
      text-decoration: none;
      margin: 0;
      box-sizing: border-box;
      display: flex;
      align-items: center;
      position: relative;

      .logo {
        font-size: 1.5rem;
        color: #fff;
        width: auto;
        overflow: hidden;
        white-space: nowrap;
        transition: width 300ms linear;
        display: flex;
        margin: 2px 0 0 0;

        span {
          display: block;
        }

        .logo-colored {
          color: transparent;
          background-image: linear-gradient(
            53deg,
            rgba(241, 87, 10, 1) 0%,
            rgba(224, 140, 112, 1) 33%,
            rgba(89, 193, 186, 1) 78%,
            rgba(0, 212, 255, 1) 100%
          );
          background-clip: text;
          -webkit-background-clip: text;
        }

        .wiki-text-clip {
          clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);

          .wiki-text {
            color: $subtitle-color-light;
          }
        }
      }

      .logo-small {
        margin: auto;
        height: 28px;
        width: 28px;
        margin: -5px 8px 0 0;
        transition: transform 300ms linear;
        animation: cog 2s linear infinite;

        &:not(:hover) {
          animation-play-state: paused;
        }
      }
    }

    .pages-list {
      display: flex;
      width: 100%;
      flex-direction: column;
      padding: 0 10px;
      box-sizing: border-box;

      @media screen and (max-width: 700px) {
        display: none;
      }

      .page-link {
        text-decoration: none;
        color: $title-color;
        padding: 8px 16px;
        margin: 4px 0;
        box-sizing: border-box;
        border-radius: 5px;
        font-weight: bold;

        &.nuxt-link-active,
        &.nuxt-link-active:hover {
          background-color: $theme-color-light;
        }

        &:hover {
          background-color: $bgcolor-alt;
        }
      }
    }
  }
}

@keyframes cog {
  0% {
    transform: rotate(360deg);
  }
  100% {
    transform: rotate(0);
  }
}
</style>
