<template>
  <div class="products__item">
    <span class="products__product-icon">
      <ion-icon v-if="product.product_kind === 'VOIP'" name="call-outline"></ion-icon>
      <ion-icon v-else-if="product.product_kind === 'WEBSITE'" name="laptop-outline"></ion-icon>
      <ion-icon v-else name="wifi-outline"></ion-icon>
    </span>
    <span class="products__product-info">{{ product.product_kind }} -
      {{ product.product_detail }}</span>
  </div>
</template>

<script>
export default {
  props: ["product"]
}
</script>
