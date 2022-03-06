<template>
  <tr class="billing-history__list-row" :class="{'billing-history__list-row--border': index < lastIndex}">
    <td>{{ bill.date }}</td>
    <td> <span class="billing-history__bill-type">{{ bill.type }}</span></td>
    <td>{{ currencySymbol }}{{ bill.amount }}</td>
    <td>{{ currencySymbol }}{{ bill.balance }}</td>
    <td>{{ bill.reference }}</td>
    <td class="billing-history__download">
      <ion-icon name="download-outline"></ion-icon>
    </td>
  </tr>
</template>

<script>
export default {
  props:["bill", "index", "lastIndex", "currencySymbol"]
}
</script>
