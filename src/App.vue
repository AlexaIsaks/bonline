<template>
  <div>
    <Header />
    <div class="site-body">
      <div class="site-body__aside">
        <Navigation />
      </div>
      <div class="site-body__main">
        <Billing />
      </div>
    </div>
  </div>
</template>

<script>
import Header from "./components/layout/Header.vue"
import Navigation from "./components/layout/Navigation.vue"
import Billing from "./components/pages/Billing.vue"

export default {
  name: 'App',
  components: {Header, Navigation, Billing}
}
</script>

<style lang="scss">
@import "style/main.scss";
</style>
