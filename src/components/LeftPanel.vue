<template>
  <div id="leftPanel">
    <h1>Business Modeling App</h1>
    <p>Backend confirmed: {{ backendConfirmed }}</p>
    <p>Backend confirmedURL: {{ backendConfirmedUrl }}</p>

  </div>
</template>

<script>
export default {
  name: 'LeftPanel',
  props: {
    backendConfirmed: String,
    backendConfirmedUrl: String
  },
  methods: {}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#leftPanel {
  background-color: #42b983;
  height: 100%;
  width: 380px;
  position: fixed;
  z-index: 1;
  top: 0;
  left: 0;
  padding: 10px
}
</style>
