<template>
  <section
    id="hero"
    class="hero"
  >
    <HomeView
      id="home"
    />
  </section>
</template>

<script>
import HomeView from '@/views/home/HomeView'

export default {
  components: {
    HomeView
  }

}
</script>

<style lang="scss" scoped>
@import './assets/scss/HeroView.scss';
</style>