<template>
  <main class="home" >
    <div class="home-img" v-if="data.heroImage">
      <img :src="$withBase(data.heroImage)" :alt="data.heroAlt || '码农说道'"/>
    </div>
    <Content class="theme-default-content custom" />
    <div v-if="data.footer" class="footer" >
      {{ data.footer }}
    </div>
  </main>
</template>

<script>
import NavLink from '@theme/components/NavLink.vue'

export default {
  name: 'Home',

  components: { NavLink },

  computed: {
    data () {
      return this.$page.frontmatter
    },
  }
}
</script>

<style lang="stylus">
.home
  padding $navbarHeight 2rem 0
  max-width $homePageWidth
  margin 0px auto
  display block
  .home-img
    text-align center
    padding 2rem
  .footer
    padding 2.5rem
    border-top 1px solid $borderColor
    text-align center
    color lighten($textColor, 25%)

@media (max-width: $MQMobileNarrow)
  .home
    padding-left 1.5rem
    padding-right 1.5rem
</style>
