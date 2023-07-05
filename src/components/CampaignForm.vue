<template>
  <section class="campaign-section">
    <form @submit.prevent="save" @keydown.enter="save">
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
    save() {
      if (this.validateForm()) {
        this.$emit('saveCampaign', this.campaign)
      }
    },
    validateForm() {
      if (!this.campaign.name) {
        alert('Please enter a campaign name.')
        return false
      }

      if (!this.campaign.keywords) {
        alert('Please enter keywords.')
        return false
      }

      if (this.campaign.amount < 100) {
        alert('Bid amount must be at least 100.')
        return false
      }

      if (!this.campaign.fund) {
        alert('Please enter a campaign fund.')
        return false
      }

      if (!this.campaign.status) {
        alert('Please select a status.')
        return false
      }

      if (!this.campaign.town) {
        alert('Please select a town.')
        return false
      }

      if (this.campaign.radius < 0) {
        alert('Radius must be a positive number or zero.')
        return false
      }

      return true
    }
  }
}
</script>
<style scoped>
form label {
  font-weight: bold;
}

form input,
form select {
  width: 100%;
  padding: 8px;
  margin-top: 8px;
  margin-bottom: 8px;
  font-size: 16px;
  border-radius: 4px;
  border: 1px solid #ccc;
  box-sizing: border-box;
  cursor: pointer;
}

form button {
  width: 100%;
  padding: 10px 20px;
  margin-top: 10px;
  background-color: #4caf50;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

form input:focus,
form select:focus {
  background-color: #f2f2f2;
}

.campaign-section {
  margin-bottom: 40px;
}
</style>
