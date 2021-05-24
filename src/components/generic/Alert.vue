<template>
  <div v-bind:class="{
    'alert': true,
    'success': (severity==='success'),
    'warning': (severity==='warning'),
    'error':(severity==='error')
  }">
    <p>
      {{ msg }}
    </p>

    <v-icon color="#4caf50 " v-if="severity==='success'">
      mdi-check
    </v-icon>
    <v-icon color="#fb8c00" v-if="severity==='warning'">
      mdi-alert
    </v-icon>
    <v-icon color="#ff5252" v-if="severity==='error'">
      mdi-alert-octagon
    </v-icon>
  </div>
</template>

<script>
export default {
  name: "Alert",
  props: {
    msg: String,
    severity: String
  }
}
</script>

<style scoped>
.alert {
  background-color: white;
  border-width: 2px;
  border-style: solid;
  display: flex;
  align-items: center;
  justify-content: space-between;
  max-width: 500px;
  padding: 10px;
  margin: 10px;
}
.success {
  border-color: #4caf50
}
.warning {
  border-color: #fb8c00
}
.error {
  border-color: #ff5252
}
</style>