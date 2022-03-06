<template>
  <!--Billing page-->
  <main class="billing" >
    <header class="billing__main-header">
      <h1 class="billing__title">Billing</h1>
      <p class="billing__description">Overview of your accounts.</p>
    </header>

    <div v-if="billing" class="billing__content">
      <!--Accounts Section-->
      <section class="billing__accounts">
        <div class="billing__account account account--active">
          <div class="account__header">
            <h2 class="account__title">Macrotel Phone</h2>
            <span class="account__active-indicator account__active-indicator--active">Active</span>
          </div>
          <span class="account__id">Account ID: 12345</span>
        </div>

        <div class="billing__account account">
          <div class="account__header">
            <h2 class="account__title">Mobis Valium</h2>
            <span class="account__active-indicator">Active</span>
          </div>
          <span class="account__id">Account ID: 12345</span>
        </div>

        <div class="billing__account account">
          <div class="account__header">
            <h2 class="account__title">Jereme Hunt 3</h2>
            <span class="account__active-indicator">Active</span>
          </div>
          <span class="account__id">Account ID: 12345</span>
        </div>
      </section>

      <!--Payment details section-->
      <section class="billing__payment-details payment-details">
        <div class="payment-details__header">
          <h2 class="payment-details__title">Payment details</h2>
          <p class="payment-details__subtitle">View details of your next invoice and payment
            method.</p>
        </div>

        <div class="payment-details__content">
          <p class="payment-details__next-invoice">Next invoice: {{ billing.nextInvoiceDate}}</p>
          
          <div class="payment-details__content-inner">
            <div class="payment-details__block payment-details__balance">
              <h3 class="payment-details__balance-title">Current balance</h3>
              <p class="payment-details__balance-amount">R{{ billing.balance }}</p>

              <div class="payment-details__block-info">
                <span class="payment-details__lock-icon">
                  <ion-icon name="lock-closed"></ion-icon>
                </span>
                <p class="payment-details__description">This is a secure 256-bit SSL encripted
                  payment. You're safe.</p>
              </div>

              <button class="payment-details__button">Pay Now</button>
            </div>

            <div class="payment-details__block">
              <div class="payment-details__method-header">
                <h3 class="payment-details__method-title">Payment method</h3>
                <span class="payment-detail__method-annual">Annual</span>
              </div>

              <div class="payment-details__block-info">
                <span class="payment-details__bulb-icon">
                  <ion-icon name="bulb"></ion-icon>
                </span>
                <p class="payment-details__description"><span
                    class="payment-details__guide">Guide: </span>To manage your payments more
                  easily, we recommend
                  switching to Direct Debit.</p>
              </div>
              <button class="payment-details__button">Switch to Direct Debit</button>
            </div>
          </div>
        </div>
      </section>

      <!--My products section-->
      <section class="billing__my-products products">
        <div class="products__header">
          <h2 class="products__title">My products</h2>
          <p class="products__subtitle">All your product at a glance.</p>
        </div> 
        <!--Products-->
        <div class="products__content">
          <template v-if="billing.products.length > 0">
            <Product v-for="product in billing.products" :product="product" :key="product.product_id"></Product>
          </template>
          <span v-else>No products</span>
        </div>
        <!--Products END-->
      </section>

      <!--Billing history section-->
      <section class="billing__history billing-history">
        <div class="billing-history__header">
          <h2 class="billing-history__title">Billing history</h2>
          <p class="billing-history__subtitle">Choose a billing plan to see more details</p>
        </div>

        <!--Billing history list-->
        <div class="billing-history__list-container">
          <table class="billing-history__list">
            <thead>
              <tr class="billing-history__list-header">
                <th>Date</th>
                <th>Type</th>
                <th>Amount</th>
                <th>Balance</th>
                <th>Reference</th>
                <th>Download</th>
              </tr>
            </thead>
          <tbody>
            <template v-if="billing.billingHistory.length > 0">
              <Bill v-for="bill in billing.billingHistory" :bill="bill" :key="bill.reference"></Bill>
            </template>
            <tr v-else class="billing-history__list-row"><td>No billing history</td></tr>
          </tbody>
          </table>
        </div>
        
        <!--Billing history list END-->
      </section>
    </div>
    <div v-else>
      <h2>No billing data available.</h2>
    </div>
  </main>
</template>

<script>
import Product from './Product.vue'
import Bill from "./Bill.vue"

export default {
  components: {Product, Bill},
  props: ["accountId"],
  data() {
    return {
      billing: null
    }
  },
  methods: {
    convertDate(date) {
      const newDate = new Date(date)
      const options = {year: 'numeric', month: 'short', day: 'numeric'}

      return newDate.toLocaleString("en_ZA", options)     
    }
  },
  mounted() {
    fetch("./data/data.json")
      .then((response) => response.json())
      .then((data) => {
          const user = data.find((user) => {
          return user.account_id === this.accountId
        })

        // const nextInvoiceDate = this.convertDate(user.next_invoice_date)
        // const products = user.products.forEach((product) =>{
        //   this.convertDate(product.date)
        // })

        this.billing = {       
          nextInvoiceDate: user.next_invoice_date,
          balance: user.balance,
          products: user.products,
          billingHistory: user.billing_history
        }
        

       
      })

      
  }

}
</script>


