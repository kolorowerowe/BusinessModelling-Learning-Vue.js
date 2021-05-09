<template>
  <div id="leftPanel">
    <h1>Business Modeling App</h1>
    <p v-if="!backendConfirmed">Backend not confirmed</p>
    <div v-if="backendConfirmed" class="div-inline">
      <p>Backend URL: {{ backendConfirmedUrl }}</p>
      <v-btn @click="editBackend" icon color="white" small>
        <v-icon >
          mdi-backspace-outline
        </v-icon>
      </v-btn>

    </div>
  </div>
</template>

<script>
export default {
  name: 'LeftPanel',
  props: {
    backendConfirmed: Boolean,
    backendConfirmedUrl: String
  },
  methods: {
    editBackend: function () {
      this.$emit('editBackend')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#leftPanel {
  background-color: #41B883;
  color: white;
  height: 100%;
  width: 380px;
  position: fixed;
  z-index: 1;
  top: 0;
  left: 0;
  padding: 10px

}
#leftPanel > h1 {
  color: #34495E;
  padding-bottom: 30px;
}
.div-inline {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
}
</style>
