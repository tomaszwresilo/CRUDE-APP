<template>
  <div>
    <header>
      <h1>Campaigns management APP 👨‍🏫</h1>
    </header>

    <section class="fund-section">
      <h2>Emerald Fund 💸</h2>
      <p><strong>Quantity:</strong> {{ emeraldFund }}</p>
    </section>

    <section class="campaign-section">
      <form @submit="saveCampaign">
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

    <main v-if="campaigns.length">
      <h2>📈 Campaigns:</h2>
      <div v-for="(campaign, index) in campaigns" :key="campaign.id" class="campaign-item">
        <h3>🚀 {{ campaign.name }}</h3>
        <p><strong>Keywords: </strong> keyword, {{ campaign.keywords }}</p>
        <p><strong>Amount:</strong> {{ campaign.amount }}</p>
        <p><strong>Fund:</strong> {{ campaign.fund }}</p>
        <p><strong>Status:</strong> {{ campaign.status }}</p>
        <p><strong>Town:</strong> {{ campaign.town }}</p>
        <p><strong>Radius:</strong> {{ campaign.radius }}</p>
        <button id="deleteButton" @click="remove(index)" v-if="index !== editedCampaignIndex">
          ❌
        </button>
        <button id="editButton" @click="edit(index)" v-if="index !== editedCampaignIndex">
          ✏️
        </button>
        <div v-if="index === editedCampaignIndex">
          <strong>Edit Mode✏️</strong>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  data() {
    return {
      campaign: {
        id: null,
        name: '',
        keywords: '',
        amount: 0,
        fund: 0,
        status: 'On',
        town: '',
        radius: 0
      },
      towns: ['Cracov', 'Warsaw', 'Wroclaw'],
      campaigns: [],
      editedCampaignIndex: null,
      emeraldFund: 1000000
    }
  },
  methods: {
    saveCampaign(event) {
      event.preventDefault()
      if (this.emeraldFund < this.campaign.fund) {
        alert('Out of money!')
        // naprawić problem kiedy jest zmiana ze 100k na 950k i pokazuje out of money
      } else {
        if (this.editedCampaignIndex !== null) {
          const updatedCampaign = { ...this.campaign }
          const previousFund = this.campaigns[this.editedCampaignIndex].fund
          this.campaigns.splice(this.editedCampaignIndex, 1, updatedCampaign)
          this.emeraldFund += previousFund
          this.emeraldFund -= parseInt(this.campaign.fund)
          this.editedCampaignIndex = null
        } else {
          this.campaign.id = Date.now()
          this.campaigns.push({ ...this.campaign })
          this.emeraldFund -= parseInt(this.campaign.fund)
        }
        this.resetForm()
      }
    },
    remove(index) {
      const removedCampaign = this.campaigns.splice(index, 1)[0]
      this.emeraldFund += parseInt(removedCampaign.fund)
    },
    edit(index) {
      this.editedCampaignIndex = index
      this.campaign = { ...this.campaigns[index] }
    },
    resetForm() {
      this.campaign = {
        id: null,
        name: '',
        keywords: '',
        amount: 0,
        fund: 0,
        status: 'On',
        town: '',
        radius: 0
      }
    }
  }
}
</script>

<style>
body {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: linear-gradient(to bottom, #f8f8f8, #e6e6e6);
}

header {
  text-align: center;
  margin-bottom: 20px;
}

h1 {
  font-size: 24px;
  color: #333;
  margin: 0;
  padding: 0;
}

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

.campaign-section {
  margin-bottom: 40px;
}

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

main {
  max-width: 100%;
  background-color: #f8f8f8;
  padding: 20px;
  border-radius: 4px;
}

h2 {
  margin-top: 0;
  font-size: 20px;
  color: #333;
}

.campaign-item {
  background-color: #fff;
  padding: 10px;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

h3 {
  margin: 0;
  margin-bottom: 10px;
  font-size: 18px;
  color: #333;
}

p {
  margin: 0;
  margin-bottom: 10px;
  margin-top: 10px;
  font-size: 16px;
  color: #555;
}

#deleteButton,
#editButton {
  margin-top: 10px;
  padding: 5px;
  font-size: 18px;
  background-color: transparent;
  border: none;
  cursor: pointer;
  outline: none;
}
</style>
