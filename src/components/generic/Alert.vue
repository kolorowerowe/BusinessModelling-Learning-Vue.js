<template>
  <div class="alert">
    <p>
      {{msg}}
    </p>
    <v-icon color="orange">
      mdi-alert
    </v-icon>
  </div>
</template>

<script>
export default {
  name: "Alert",
  props: {
    msg: String
  }
}
</script>

<style scoped>
.alert {
  background-color: white;
  border: 2px solid #ff9800;
  display: flex;
  align-items: center;
  justify-content: space-between;
  max-width: 500px;
  padding: 10px;
  margin: 10px;
}
</style>