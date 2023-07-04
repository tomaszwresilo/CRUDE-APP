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
