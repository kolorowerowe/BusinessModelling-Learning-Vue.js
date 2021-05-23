<template>
  <v-app id="app">

    <LeftPanel :backendConfirmed="backendConfirmed"
               :backendConfirmedUrl="backendConfirmedUrl"
               v-on:editBackend="editBackend"
               :fileConfirmed="fileConfirmed"
               v-on:editFile="editFile"
               v-on:applyFilter="applyFilter"
               :route="route"
               v-on:setRoute="setRoute"/>

    <v-main id="mainDiv">
      <Home v-if="route==='HOME'"/>

      <ConnectBackend v-if="route === 'BACKEND'"
                      v-on:confirmBackend="confirmBackend"/>

      <SelectFile v-if="route==='FILE'"
                  v-on:confirmFile="confirmFile"/>

      <ChartContent v-if="route==='CHART'"
                   :backendConfirmedUrl="backendConfirmedUrl"
                   :fileData="fileData"
                   :columns="columns"
                   :minNodeValue="minNodeValue"
      />
    </v-main>

  </v-app>

</template>

<script>
import ConnectBackend from './components/routes/ConnectBackend.vue';
import LeftPanel from './components/LeftPanel.vue';
import ChartContent from './components/routes/ChartContent.vue';
import SelectFile from "./components/routes/SelectFile";
import Home from "./components/routes/Home";

export default {
  name: 'App',
  components: {
    LeftPanel,
    Home,
    SelectFile,
    ConnectBackend,
    ChartContent
  },
  methods: {
    confirmBackend: function (backendUrl) {
      this.backendConfirmedUrl = backendUrl;
      this.backendConfirmed = true;
    },
    editBackend: function () {
      this.backendConfirmed = false;
    },
    confirmFile: function (fileData, columns) {
      this.fileData = fileData;
      this.columns = columns;
      this.fileConfirmed = true
    },
    editFile: function () {
      this.fileConfirmed = false;
    },
    applyFilter: function (minNodeValue) {
      this.minNodeValue = minNodeValue;
    },
    setRoute: function (newRoute) {
      this.route = newRoute;
    }
  },
  data() {
    return {
      route: 'HOME',
      backendConfirmed: false,
      backendConfirmedUrl: '',
      fileConfirmed: false,
      fileData: undefined,
      columns: ['Case ID', 'Activity', 'Start Timestamp'],
      minNodeValue: 0
    }
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

.div-inline {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
}

#mainDiv {
  margin-left: 250px;
}

.input {
  min-width: 500px;
  padding: 12px 20px;
  margin: 8px;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}
</style>
