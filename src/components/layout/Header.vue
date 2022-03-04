<template>
  <!--Site header-->
  <header class="site-header">
    <img src="../../assets/brand/bonline-logo.svg" alt="bOnline logo"
      class="site-header__bonline-logo">


    <div class="site-header__user-container">
      <!--Site notfication-->
      <div class="site-header__notification-container">
        <span class="site-header__notification-icon">
          <ion-icon name="notifications-outline"></ion-icon>
        </span>
        <span class="site-header__notification-indicator"></span>
      </div>

      <!--User-->
      <div class="site-header__user">
        <div class="site-header__avatar-container">
          <img src="../../assets/avatar.png" alt="name surname" class="site-header__avatar">
        </div>
        <div class="site-header__user-details">
          <span class="site-header__user-fullname">First Lastname</span>
          <span class="site-header__user-email">firstlastname@email.com</span>
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

}
</script>

<style>

</style>