<template>
  <div id="connectBackend">
    <h3>Enter your backend address</h3>
    <input v-model="backendUrl" placeholder="edit me" class="backend-input">
    <button @click="connectToBackend">Connect to backend</button>
  </div>
</template>

<script>
export default {
  name: 'WelcomeScreen',
  data() {
    return {
      backendUrl: ''
    }
  },
  props: {
    msg: String,
  },
  methods: {
    connectToBackend: function (){
      this.$emit('confirmBackend', this.backendUrl)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#connectBackend {
  margin-left: 400px;
}
.backend-input {
  margin-top: 10px;
}
</style>
