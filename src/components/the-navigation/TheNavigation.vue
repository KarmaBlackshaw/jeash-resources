<template>
  <div
    class="navigation"
    :class="{
      'navigation--darker': windowScrollY > 5
    }"
  >
    <div class="navigation__container">
      <TheNavigationHamburger
        class="navigation__hamburger"
        @click="toggleHamburger"
      />

      <div class="navigation__logo">
        <router-link to="/">
          Ernie Jeash
        </router-link>
      </div>

      <div class="navigation__aside">
        asd
      </div>
    </div>
  </div>
</template>

<script>
import { reactive, ref, inject } from 'vue'
import { useRoute } from 'vue-router'
import { useEventListener } from '@vueuse/core'

import TheNavigationHamburger from './components/TheNavigationHamburger'
import _throttle from 'lodash/throttle'

export default {
  components: {
    TheNavigationHamburger
  },

  setup () {
    const tabs = reactive([
      {
        text: 'Join Discord',
        to: '#contact',
        type: 'button'
      }
    ])

    const windowScrollY = ref(0)
    useEventListener(window, 'scroll', _throttle(e => {
      const windowInstance = e.path[1]

      windowScrollY.value = windowInstance.scrollY
    }, 100))

    const isHamburgerActive = ref(false)
    function toggleHamburger () {
      isHamburgerActive.value = !isHamburgerActive.value
    }

    return {
      breakpoint: inject('breakpoint'),

      route: useRoute(),

      tabs,
      windowScrollY,

      isHamburgerActive,
      toggleHamburger
    }
  }
}
</script>

<style lang="scss" scoped>
@import './assets/scss/TheNavigation';
</style>