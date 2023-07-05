<template>
  <div id="wrapper">
    <header>
      <h1>Campaigns Management APP 👨‍🏫</h1>
    </header>
    <ModalFullScreen :textValue="enterKeyText" />
    <EmeraldFund :emeraldFund="emeraldFund" />

    <CampaignForm :campaign="campaign" :towns="towns" @saveCampaign="saveCampaign" />
    <ModalFullScreen v-if="outOfMoney" :textValue="outOfMoneyText" />
    <CampaignList
      :campaigns="campaigns"
      :editedCampaignIndex="editedCampaignIndex"
      @remove="remove"
      @edit="edit"
      @sortBy="handleSortBy"
    />
  </div>
</template>

<script>
import EmeraldFund from '/src/components/EmeraldFund.vue'
import CampaignForm from '/src/components/CampaignForm.vue'
import CampaignList from '/src/components/CampaignList.vue'
import ModalFullScreen from '/src/components/ModalFullScreen.vue'

export default {
  components: {
    EmeraldFund,
    CampaignForm,
    CampaignList,
    ModalFullScreen
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
      enterKeyText: 'You can also use Enter key to add campaign 😉',
      outOfMoneyText: 'Out of money!',
      towns: ['Cracov', 'Warsaw', 'Wroclaw'],
      campaigns: [],
      editedCampaignIndex: null,
      emeraldFund: 1000000,
      outOfMoney: false
    }
  },
  methods: {
    saveCampaign(campaign) {
      event.preventDefault()
      if (this.emeraldFund < campaign.fund) {
        this.outOfMoney = true
      } else {
        this.outOfMoney = false
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
    handleSortBy(key) {
      this.sortBy(key)
    },
    sortBy(key) {
      this.campaigns.sort((a, b) => {
        if (a[key] < b[key]) return -1
        if (a[key] > b[key]) return 1
        return 0
      })
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

h2 {
  margin-top: 0;
  font-size: 20px;
  color: #333;
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

#wrapper {
  background-color: white;
  padding: 20px;
  border-radius: 20px;
}

@media only screen and (max-width: 600px) {
  body {
    background-image: none;
  }
}
</style>
