<template>
  <!--Billing page-->
  <main class="billing">
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
            <div class="payment-details__block">
              <h3 class="payment-details__balance-title">Current balance</h3>
              <p class="payment-details__balance-amount">{{ billing.currencySymbol }}{{ billing.balance }}</p>

              <div class="payment-details__block-info">
                <span class="payment-details__lock-icon">
                  <ion-icon name="lock-closed"></ion-icon>
                </span>
                <p class="payment-details__description">This is a secure 256-bit SSL encripted
                  payment. You're safe.</p>
              </div>
              <a href="#" class="payment-details__button">Pay Now</a>
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
                <p class="payment-details__description"><span class="payment-details__guide">Guide:
                  </span>To manage your payments more
                  easily, we recommend
                  switching to Direct Debit.</p>
              </div>
              <a href="#" class="payment-details__button">Switch to Direct Debit</a>
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
            <Product v-for="product in billing.products" :product="product"
              :key="product.product_id"></Product>
          </template>
          <div v-else class="billing__message-container">
              <h3 class="billing__message">No products available.</h3>
          </div>
          
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
        <template v-if="billing.billingHistory.length > 0">
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
                <Bill v-for="(bill, index) in billing.billingHistory" :bill="bill"
                  :currencySymbol="billing.currencySymbol" :index="index" :lastIndex="billing.billingHistory.length - 1" :key="bill.reference"></Bill>            
            </tbody>
          </table>
        </div>
      </template>
      <div v-else class="billing__message-container">
        <h3 class="billing__message">No billing history available.</h3>
      </div>

        <!--Billing history list END-->
      </section>
    </div>
    <div v-else-if="billingError" class="billing__message-container">
      <h2 class="billing__message">An error has occurred.</h2>
    </div>
    <div v-else class="billing__message-container">
      <h2 class="billing__message">No billing information available.</h2>
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
      billingError: false,
      billing: null
    }
  },
  methods: {
    convertDateFormat(date) {
      const newDate = new Date(date)
      const options = {year: 'numeric', month: 'short', day: 'numeric'}

      return newDate.toLocaleString("en-ZA", options)     
    },
    getCurrencySymbol(country) {
      if (country === "UNITED KINGDOM") {
        return "\u00A3"
      } else if (country === "SOUTH AFRICA") {
        return "R"
      }
    }
  },
  mounted() {
    fetch("./data/data.json")
      .then((response) => response.json())
      .then((data) => {
        const user = data.find((user) => {
          return user.account_id === this.accountId
        })

        const currencySymbol = this.getCurrencySymbol(user.address_country)
        const nextInvoiceDate = this.convertDateFormat(user.next_invoice_date)
        // Change date formate and change balance and amount to floats
        if (user.billing_history.length > 0) {
          user.billing_history.forEach((bill) => {
          bill.date = this.convertDateFormat(bill.date);
          bill.amount = bill.amount.toFixed(2)
          bill.balance = bill.balance.toFixed(2)
        })
        }

        // Captilize product kind
        if (user.products.length > 0) {
          user.products.forEach((product) => {
            if (product.product_kind === "VOIP") {
              product.product_kind = "VoIP"
            } else {
               const product_kind = product.product_kind.toLowerCase()
               product.product_kind = product_kind[0].toUpperCase() + product_kind.slice(1)
            }
          })
        }
        
        this.billing = {
          currencySymbol,
          nextInvoiceDate,
          balance: user.balance.toFixed(2),
          products: user.products,
          billingHistory: user.billing_history
        }

        this.billingError = false
      }, (error) => {
          this.billingError = true
      })

      
  }

}
</script>


