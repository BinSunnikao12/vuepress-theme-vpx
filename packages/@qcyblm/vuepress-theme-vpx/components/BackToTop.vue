<template>
  <transition name="fade">
    <i
      v-if="show"
      class="go-to-top fa fa-lg fa-arrow-up"
      aria-hidden="true"
      @click="scrollToTop"
    >
    </i>
  </transition>
</template>

<script>
import debounce from 'lodash.debounce'
export default {
  name: 'BackToTop',
  props: {
    threshold: {
      type: Number,
      default: 300
    }
  },
  data () {
    return {
      scrollTop: null
    }
  },
  computed: {
    show () {
      return this.scrollTop > this.threshold
    }
  },
  mounted () {
    this.scrollTop = this.getScrollTop()
    window.addEventListener('scroll', debounce(() => {
      this.scrollTop = this.getScrollTop()
    }, 100))
  },
  methods: {
    getScrollTop () {
      return window.pageYOffset
        || document.documentElement.scrollTop
        || document.body.scrollTop || 0
    },
    scrollToTop () {
      window.scrollTo({ top: 0, behavior: 'smooth' })
      this.scrollTop = 0
    }
  }
}
</script>

<style lang="stylus">
.go-to-top
  position fixed
  width 32px
  height 32px
  line-height 32px
  text-align center
  border-radius 50%
  bottom 2.2rem
  right 2.5rem
  color $accentColor
  z-index 1
  transition all 0.5s
  vertical-align bottom
  cursor pointer
.go-to-top:hover
  color lighten($accentColor, 30%)
.fade-enter-active, .fade-leave-active
  transition opacity 0.3s
.fade-enter, .fade-leave-to
  opacity 0
@media (max-width: $MQMobile)
  .go-to-top
    bottom: 1rem;
    right: 1rem;
[data-theme = dark ] & {
  .go-to-top {
  color: $dark[--accentColor]
  }
  .go-to-top:hover {
  color: lighten($dark[--accentColor], 30%)
  }
}
</style>