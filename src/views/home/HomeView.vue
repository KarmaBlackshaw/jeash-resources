<template>
  <section class="home">
    <div class="home__background"></div>

    <base-scroll-icon class="home__scroll-icon" />

    <div class="home__container">
      <div class="home__introduction introduction">
        <div class="introduction__title mb-5">
          <p>Change your lens.</p>
          <p>Change your story.</p>
        </div>

        <div class="introduction__subtitle mb-5">
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Consequuntur, iusto nesciunt, autem eaque quae id obcaecati ullam ab quibusdam veniam quaerat architecto sapiente quia temporibus! Placeat expedita amet vero in!
        </div>

        <div class="introduction__actions">
          <button
            class="btn"
            @click="$router.push({hash: '#contact'})"
          >
            Book Now
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { inject } from 'vue'

export default {
  setup () {
    const breakpoint = inject('breakpoint')

    return {
      breakpoint
    }
  }
}
</script>

<style src="./assets/scss/HomeView.scss" lang="scss" scoped></style>