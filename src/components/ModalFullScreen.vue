<template>
  <div class="backdrop" v-if="statusHide">
    <div class="modal">
      <h2>Campaigns Management ✨</h2>
      <p :class="{ 'red-text': textValue === 'Out of money!' }">{{ textValue }}</p>
      <button @click="hide">X</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    textValue: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      statusHide: true
    }
  },
  methods: {
    hide(statusHide) {
      this.statusHide = !statusHide
    }
  }
}
</script>
<style scoped>
p {
  font-size: 20px;
}
span {
  cursor: pointer;
}

button {
  all: unset;
  color: black;
  padding: 8px 16px;
  font-size: 14px;
  background-color: #f3f3f3;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #e0e0e0;
}

.modal {
  width: 400px;
  padding: 20px;
  margin: 0 auto;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: white;
  border-radius: 18px;
  text-align: center;
}

.backdrop {
  margin: 0 auto;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  position: fixed;
  background: rgba(0, 0, 0, 0.5);
  width: 100%;
  height: 100%;
}
.red-text {
  color: red;
}
</style>
