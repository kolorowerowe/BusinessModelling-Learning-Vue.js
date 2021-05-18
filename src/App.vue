<template>
  <v-app id="app">
    <v-main id="mainDiv">
      <LeftPanel :backendConfirmed="backendConfirmed"
                 :backendConfirmedUrl="backendConfirmedUrl"
                 v-on:editBackend="editBackend"
                 :fileConfirmed="fileConfirmed"
                 v-on:editFile="editFile"/>
      <ConnectBackend v-if="!backendConfirmed"
                      v-on:confirmBackend="confirmBackend"/>

      <SelectFile v-else-if="!fileConfirmed"
                  v-on:confirmFile="confirmFile"/>

      <MainContent v-else
                   :backendConfirmedUrl="backendConfirmedUrl"
                   :fileData="fileData"
                   :columns="columns"
      />
    </v-main>
  </v-app>

</template>

<script>
import ConnectBackend from './components/ConnectBackend.vue';
import LeftPanel from './components/LeftPanel.vue';
import MainContent from './components/MainContent.vue';
import SelectFile from "./components/SelectFile";

export default {
  name: 'App',
  components: {
    SelectFile,
    ConnectBackend,
    LeftPanel,
    MainContent
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
  },
  data() {
    return {
      backendConfirmed: false,
      backendConfirmedUrl: '',
      fileConfirmed: false,
      fileData: undefined,
      columns: ['Case ID', 'Activity', 'Start Timestamp']
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
  display: flex;
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
