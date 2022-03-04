<template>
  <!--Billing page-->
  <main class="billing">
    <header class="billing__main-header">
      <h1 class="billing__title">Billing</h1>
      <p class="billing__description">Overview of your accounts.</p>
    </header>

    <div class="billing__content">
      <!--Accounts Section-->
      <section class="billing__accounts">
        <div class="account account--active">
          <div class="account__header">
            <h2 class="account__title">Macrotel Phone</h2>
            <span class="account__active-indicator account__active-indicator--active">Active</span>
          </div>
          <span class="account__id">Account ID: 12345</span>
        </div>

        <div class="account">
          <div class="account__header">
            <h2 class="account__title">Mobis Valium</h2>
            <span class="account__active-indicator">Active</span>
          </div>
          <span class="account__id">Account ID: 12345</span>
        </div>

        <div class="account">
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
          <p class="payment-details__description">View details of your next invoice and payment
            method.</p>
        </div>

        <div class="payment-details__content">
          <p class="payment-details__next-invoice">Next invoice: 10 Feb 2022</p>
          <div class="payment-details__content-inner">

            <div class="payment-details__balance">
              <h3 class="payment-details__balance-title">Current balance</h3>
              <p class="payment-details__balance-amount">R59.00</p>

              <div class="payment-details__discription-container">
                <span class="payment-details__lock-icon">
                  <ion-icon name="lock-closed"></ion-icon>
                </span>
                <p class="payment-details__description">This is a secure 256-bit SSL encripted
                  payment. You're safe.</p>
              </div>

              <button class="payment-details__button">Pay Now</button>
            </div>

            <div class="payment-details__method">
              <div class="payment-details__method-header">
                <h3 class="payment-details__method-title">Payment method</h3>
                <span class="payment-detail__method-annual">Annual</span>
              </div>

              <div class="payment-details__discription-container">
                <span class="payment-details__bulb-icon">
                  <ion-icon name="bulb"></ion-icon>
                </span>
                <p class="payment-details__description"><strong
                    class="payment-details__guide">Guide:</strong> To manage your payments more
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
          <p class="products__description">All your product at a glance.</p>
        </div>

        <div class="products__content">
          <div class="products__item">
            <span class="products__product-icon">
              <ion-icon name="call-outline"></ion-icon>
            </span>
            <span class="products__product-info">VolP - 902903393939</span>
          </div>
          <div class="products__item">
            <span class="products__product-icon">
              <ion-icon name="wifi-outline"></ion-icon>
            </span>
            <span class="products__product-info">Fibre - SW29BE</span>
          </div>
          <div class="products__item">
            <span class="products__product-icon">
              <ion-icon name="laptop-outline"></ion-icon>
            </span>
            <span class="products__product-info">Website - wwww.website.com</span>
          </div>
        </div>
      </section>

      <!--Billing history section-->
      <section class="billing__history billing-history">
        <div class="billing-history__header">
          <h2 class="billing-history__title">Billing history</h2>
          <p class="billing-history__description">Choose a billing plan to see more details</p>
        </div>

        <table class="billing-history__list">
          <tr class="billing-history__list-header">
            <th>Date</th>
            <th>Type</th>
            <th>Amount</th>
            <th>Balance</th>
            <th>Reference</th>
            <th>Download</th>
          </tr>
          <tr>
            <td>13 Dec 2021</td>
            <td>Invoice</td>
            <td>R8.00</td>
            <td>R45.00</td>
            <td>1234abcd</td>
            <td class="billing-history__download">
              <ion-icon name="download-outline"></ion-icon>
            </td>
          </tr>
          <tr>
            <td>13 Dec 2021</td>
            <td>Invoice</td>
            <td>R8.00</td>
            <td>R45.00</td>
            <td>1234abcd</td>
            <td class="billing-history__download">
              <ion-icon name="download-outline"></ion-icon>
            </td>
          </tr>
          <tr>
            <td>13 Dec 2021</td>
            <td>Invoice</td>
            <td>R8.00</td>
            <td>R45.00</td>
            <td>1234abcd</td>
            <td class="billing-history__download">
              <ion-icon name="download-outline"></ion-icon>
            </td>
          </tr>
        </table>
      </section>
    </div>
  </main>
</template>
