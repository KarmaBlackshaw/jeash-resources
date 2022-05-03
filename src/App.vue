<template>
  <div
    class="app"
  >
    <div class="app__header">
      <TheNavigation class="app__navigation" />
    </div>

    <div class="app__body">
      <router-view />
    </div>

    <div class="app__footer">
      <TheFooter />
    </div>
  </div>
</template>

<script>
import { ref, provide, nextTick, onMounted } from 'vue'
import { useRoute } from 'vue-router'

// composables
import useBreakpoint from '@/composables/useBreakpoint'

import TheNavigation from './components/the-navigation/TheNavigation'
import TheFooter from './components/the-footer/TheFooter'
import Loader from '@/views/loader/LoaderView'

export default {
  components: {
    TheNavigation,
    TheFooter,
    Loader
  },

  setup () {
    const {
      breakpoint
    } = useBreakpoint()

    provide('breakpoint', breakpoint)

    onMounted(async () => {
      function loadJS (options = {}) {
        return new Promise((resolve, reject) => {
          const scriptEle = document.createElement("script")

          for (const key in options) {
            scriptEle.setAttribute(key, options[key])
          }

          document.body.appendChild(scriptEle)

          scriptEle.addEventListener("load", () => resolve())
          scriptEle.addEventListener("error", err => reject(err))
        })
      }

      function statusChangeCallback (response) { // Called with the results from FB.getLoginStatus().
        console.log('statusChangeCallback')
        console.log(response) // The current login status of the person.
        if (response.status === 'connected') { // Logged into your webpage and Facebook.
          testAPI()
        } else { // Not logged into your webpage or we are unable to tell.
          console.log(response)
        }
      }

      function checkLoginState () { // Called when a person is finished with the Login Button.
        window.FB.getLoginStatus(function (response) { // See the onlogin handler
          statusChangeCallback(response)
        })
      }

      window.fbAsyncInit = function () {
        window.FB.init({
          appId      : '401372528255570',
          cookie     : true, // Enable cookies to allow the server to access the session.
          xfbml      : true, // Parse social plugins on this webpage.
          version    : 'v13.0' // Use this Graph API version for this call.
        })

        window.FB.getLoginStatus(function (response) { // Called after the JS SDK has been initialized.
          statusChangeCallback(response) // Returns the login status.
        })
      }

      function testAPI () {
        console.log('Welcome!  Fetching your information.... ')
        window.FB.api('/me', function (response) {
          console.log('Successful login for: ' + response.name)
          document.getElementById('status').innerHTML =
        'Thanks for logging in, ' + response.name + '!'
        })
      }

      await loadJS({
        src: 'https://connect.facebook.net/en_US/sdk.js',
        async: true,
        defer: true,
        crossorigin: 'anonymous'
      })
    })
  }
}
</script>

<style lang="scss">
@import './assets/scss/view/App';
</style>
