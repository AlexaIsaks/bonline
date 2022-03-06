<template>
  <tr class="billing-history__list-row">
    <td>{{ bill.date }}</td>
    <td> <span class="billing-history__bill-type">{{ bill.type }}</span></td>
    <td>R{{ bill.amount }}</td>
    <td>R{{ bill.balance }}</td>
    <td>{{ bill.reference }}</td>
    <td class="billing-history__download">
      <ion-icon name="download-outline"></ion-icon>
    </td>
  </tr>
</template>

<script>
export default {
  props:["bill"]
}
</script>
