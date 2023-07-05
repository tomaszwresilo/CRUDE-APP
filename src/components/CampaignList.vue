<template>
  <main v-if="campaigns.length">
    <h2>📈 Campaigns:</h2>
    <div class="sort-buttons">
      <button @click="sortBy('name')">🡓 Sort by Name</button>
      <button @click="sortBy('radius')">🡓 Sort by Radius</button>
      <button @click="sortBy('amount')">🡓 Sort by Amount</button>
    </div>
    <div v-for="(campaign, index) in campaigns" :key="campaign.id" class="campaign-item">
      <h2>🚀 {{ campaign.name }}</h2>
      <p><strong>Keywords: </strong> keyword, {{ campaign.keywords }}</p>
      <p><strong>Amount:</strong> {{ campaign.amount }}</p>
      <p><strong>Fund:</strong> {{ campaign.fund }}</p>
      <p><strong>Status:</strong> {{ campaign.status }}</p>
      <p><strong>Town:</strong> {{ campaign.town }}</p>
      <p><strong>Radius:</strong> {{ campaign.radius }}</p>
      <button
        name="deleteButton "
        id="deleteButton"
        @click="remove(index)"
        v-if="index !== editedCampaignIndex"
      >
        ❌
      </button>
      <button
        name="editButton"
        id="editButton"
        @click="edit(index)"
        v-if="index !== editedCampaignIndex"
      >
        ✏️
      </button>
      <div id="editMode" v-if="index === editedCampaignIndex">
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
    },
    sortBy(key) {
      this.$emit('sortBy', key)
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

button {
  padding: 10px 20px;
  background-color: #4caf50;
  margin: 5px;
  margin-bottom: 10px;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 9px;
  color: #fff;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.4);
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

#editMode {
  text-align: center;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  padding: 10px;
}
@media only screen and (max-width: 600px) {
  button {
    display: flex;
    justify-content: center;
    width: 100%;
    height: 20%;
    font-size: 12px;
    text-align: center;
  }
}
</style>
