<template>
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
      <button id="editButton" @click="edit(index)" v-if="index !== editedCampaignIndex">✏️</button>
      <div v-if="index === editedCampaignIndex">
        <strong>Edit Mode✏️</strong>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  props: {
    campaigns: {
      type: Array,
      required: true
    },
    editedCampaignIndex: {
      type: Number,
      default: null
    }
  },
  methods: {
    remove(index) {
      this.$emit('remove', index)
    },
    edit(index) {
      this.$emit('edit', index)
    }
  }
}
</script>

<style scoped>
main {
  max-width: 100%;
  background-color: #f8f8f8;
  padding: 20px;
  border-radius: 4px;
}
.campaign-item {
  background-color: #fff;
  padding: 10px;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
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
