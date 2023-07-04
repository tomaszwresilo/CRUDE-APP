<template>
  <section class="campaign-section">
    <form @submit="save">
      <label for="name">📄 Campaign Name:</label>
      <input type="text" id="name" v-model="campaign.name" required /><br />

      <label for="keywords">💬 Keywords:</label>
      <input type="text" id="keywords" v-model="campaign.keywords" required /><br />

      <label for="bidAmount">💵 Bid Amount:</label>
      <input type="number" id="bidAmount" v-model="campaign.amount" min="100" required /><br />

      <label for="fund">💸 Campaign Fund:</label>
      <input type="number" id="fund" v-model="campaign.fund" required /><br />

      <label for="status">📌 Status:</label>
      <select id="status" v-model="campaign.status" required>
        <option value="On">On</option>
        <option value="Off">Off</option></select
      ><br />

      <label for="town">🏠 Town:</label>
      <select id="town" v-model="campaign.town" required>
        <option v-for="town in towns" :value="town" :key="town">{{ town }}</option></select
      ><br />

      <label for="radius">📍 Radius (km):</label>
      <input id="radius" v-model="campaign.radius" type="number" min="0" required /><br />

      <button type="submit">Enter</button>
    </form>
  </section>
</template>

<script>
export default {
  props: {
    campaign: {
      type: Object,
      required: true
    },
    towns: {
      type: Array,
      required: true
    }
  },
  methods: {
    saveCampaign(event) {
      event.preventDefault()

      // Zaktualizuj obiekt campaign przy użyciu localStatus
      this.campaign.status = this.localStatus

      // Wyemituj zdarzenie, aby poinformować komponent nadrzędny o zmianie
      this.$emit('campaign-updated', this.campaign)

      // Zresetuj formularz
      this.resetForm()
    }
    // ...
  }
}
</script>
