<template>
  <div id="wrapper">
    <header>
      <h1>Campaigns management APP 👨‍🏫</h1>
    </header>

    <EmeraldFund :emeraldFund="emeraldFund" />

    <CampaignForm :campaign="campaign" :towns="towns" @saveCampaign="saveCampaign" />

    <CampaignList
      :campaigns="campaigns"
      :editedCampaignIndex="editedCampaignIndex"
      @remove="remove"
      @edit="edit"
    />
  </div>
</template>

<script>
import EmeraldFund from '/src/components/EmeraldFund.vue'
import CampaignForm from '/src/components/CampaignForm.vue'
import CampaignList from '/src/components/CampaignList.vue'

export default {
  components: {
    EmeraldFund,
    CampaignForm,
    CampaignList
  },
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
    saveCampaign(campaign) {
      event.preventDefault()
      if (this.emeraldFund < campaign.fund) {
        alert('Out of money!')
      } else {
        if (this.editedCampaignIndex !== null) {
          const updatedCampaign = { ...campaign }
          const previousFund = this.campaigns[this.editedCampaignIndex].fund
          this.campaigns.splice(this.editedCampaignIndex, 1, updatedCampaign)
          this.emeraldFund += previousFund
          this.emeraldFund -= parseInt(campaign.fund)
          this.editedCampaignIndex = null
        } else {
          campaign.id = Date.now()
          this.campaigns.push({ ...campaign })
          this.emeraldFund -= parseInt(campaign.fund)
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
  background-image: url('./src/img/stacked-peaks-haikei.svg');
  background-repeat: repeat-x;
  background-color: #f3f3f3;
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

#wrapper {
  background-color: white;
  padding: 20px;
  border-radius: 20px;
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

@media only screen and (max-width: 600px) {
  body {
    background-image: none;
  }
}
</style>
