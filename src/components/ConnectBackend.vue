<template>
  <div id="connectBackend">
    <h3>Enter your backend address</h3>
<!--    <v-text-field v-model="backendUrl"-->
<!--                  placeholder="Edit me"-->
<!--                  label="Backend URL"-->
<!--    >-->
<!--    </v-text-field>-->
        <input v-model="backendUrl" placeholder="Enter back-end URL" class="input">
    <v-btn @click="connectToBackend"
           class="text-white"
           color="#34495E"
    >
      Connect to backend
      <v-icon dark right>
        mdi-checkbox-marked-circle
      </v-icon>
    </v-btn>
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
  methods: {
    connectToBackend: function () {
      if (this.backendUrl) {
        this.$emit('confirmBackend', this.backendUrl)
      } else {
        alert('Backend URL is empty');
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#connectBackend {
  margin-left: 300px;
}

.backend-input {
  min-width: 500px;
  padding: 12px 20px;
  margin: 8px;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}
</style>
