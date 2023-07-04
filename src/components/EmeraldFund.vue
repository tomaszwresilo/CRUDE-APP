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

<style scoped>
.fund-section {
  text-align: center;
  margin: 10px;
}

.fund-section h2 {
  margin-bottom: 10px;
}

.fund-section p {
  margin-bottom: 0;
  font-size: 18px;
  color: #333;
}
</style>
