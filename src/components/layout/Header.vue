<template>
  <!--Site header-->
  <header class="site__header site-header">
    <div class="site-header__bonline-logo">
      <img src="../../assets/brand/bonline-logo.svg" alt="bOnline logo" class="bonline-logo">
    </div>

    <div class="site-header__user-container">
      <!--Site notfication-->
      <div class="site-header__notification-container">
        <span class="site-header__notification-icon">
          <ion-icon name="notifications-outline"></ion-icon>
        </span>
        <span v-if="notification" class="site-header__notification-indicator"></span>
      </div>

      <!--User-->
      <div class="site-header__user">
        <div class="site-header__avatar-container">
          <img src="../../assets/avatar.png" alt="avatar" class="site-header__avatar">
        </div>
        <div class="site-header__user-details">
          <span v-if="user" class="site-header__user-fullname">{{ user.firstName }}
            {{ user.lastName}}</span>
          <span v-if="user" class="site-header__user-email">{{ user.emailAddress }}</span>
        </div>

        <span class="site-header__chevron-down">
          <ion-icon name="chevron-down-outline"></ion-icon>
        </span>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  props: ["user", "notification"]
}
</script>