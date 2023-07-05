<template>
  <div class="backdrop" v-if="statusHide">
    <div class="modal">
      <h2>Campaigns Management ✨</h2>
      <p>You can also use Enter key to add campaign 😉</p>
      <button @click="hide">X</button>
    </div>
  </div>
</template>

<script>
export default {
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
span {
  cursor: pointer;
}

button {
  all: unset;
  color: #4caf50;
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
</style>
