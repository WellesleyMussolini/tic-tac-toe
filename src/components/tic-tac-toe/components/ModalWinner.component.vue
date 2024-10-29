<template>
  <div v-if="visibility">
    <div class="modal-overlay" @click="closeModal"></div>
    <div id="modal" class="modal-container">
      <div class="modal-content">
        <button class="close-button" @click="closeModal">✖</button>
        <p>{{ message }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    visibility: {
      required: true,
      type: Boolean,
      default: false,
    },
    message: {
      required: true,
      type: String,
    },
  },
  methods: {
    closeModal() {
      this.$emit("close"); // Emit an event to indicate the modal should close
    },
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.6); /* Semi-transparent black */
  z-index: 30;
}

.modal-container {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 40;
  animation: fadeIn 0.3s ease-out;
}

.modal-content {
  background: #fff;
  padding: 20px 40px;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
  color: gray;
  font-size: 1.5rem;
  text-align: center;
  animation: scaleUp 0.3s ease-out;
  position: relative;
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
}

.close-button {
  position: absolute;
  top: 10px;
  right: 10px;
  background: none;
  border: none;
  font-size: 1.5rem;
  color: black;
  cursor: pointer;
}

/* Animations */
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes scaleUp {
  from {
    transform: scale(0.9);
  }
  to {
    transform: scale(1);
  }
}
</style>
