<template>
  <section class="fund-section">
    <h2>Emerald Fund 💸</h2>
    <p><strong>Quantity:</strong> {{ emeraldFund }}</p>
  </section>
</template>

<script>
export default {
  props: {
    emeraldFund: {
      type: Number,
      required: true
    }
  }
}
</script>
