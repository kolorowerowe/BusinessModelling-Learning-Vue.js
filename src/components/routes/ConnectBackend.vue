<template>
  <div>
    <h3>Enter your backend address</h3>
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

    <Alert v-if="!!successMessage" :msg="successMessage" severity="success"></Alert>
    <Alert v-if="!!errorMessage" :msg="errorMessage" severity="error"></Alert>

  </div>
</template>

<script>
import axios from "axios";
import Alert from "../generic/Alert";

export default {
  name: 'WelcomeScreen',
  props: {
    backendConfirmedUrl: String
  },
  data() {
    return {
      backendUrl: this.backendConfirmedUrl,
      successMessage: '',
      errorMessage: ''
    }
  },
  components: {
    Alert
  },
  methods: {
    connectToBackend() {
      this.successMessage = '';
      this.errorMessage = '';

      if (this.backendUrl) {
        this.loading = true;
        axios
            .get(`${this.backendUrl}`)
            .then(({data}) => {
              if (data.status === 'OK') {
                this.$emit('confirmBackend', this.backendUrl)
                this.successMessage = 'Backend responded with OK';
              } else {
                this.errorMessage = 'Backend URL did not respond with OK status!';
              }
            })
            .catch(err => {
              this.errorMessage = 'Backend URL responded with error: ' + err.message;
            })
      } else {
        this.errorMessage = 'Backend URL is empty!';
      }

    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


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
