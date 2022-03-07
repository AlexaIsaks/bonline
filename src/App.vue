<template>
  <div class="site">
    <Header :user="user" :notification="notification" />
    <div class="site__inner">
      <div class="site__aside">
        <Navigation />
      </div>
      <div class="site__main">
        <Billing :accountId="accountId" />
      </div>
    </div>
  </div>
</template>

<script>
import Header from "./components/layout/Header.vue"
import Navigation from "./components/layout/Navigation.vue"
import Billing from "./components/pages/Billing/Billing.vue"

export default {
  name: 'App',
  components: {
    Header,
    Navigation,
    Billing
  },
  data() {
    return {
      accountId: 291321,
      notification: true,
      user: null
    }
  },
  mounted() {
    fetch("./data/data.json")
      .then((response) => response.json())
      .then((data) => {
        const user = data.find((user) => {
          return user.account_id === this.accountId
        })

        this.user = {
          firstName: user.first_name,
          lastName: user.last_name,
          emailAddress: user.email_address
        }
      })
  }
}
</script>

<style lang="scss">
@import "style/main.scss";
</style>
