<template>
  <div id="mainDiv">
    <LeftPanel :backendConfirmed="backendConfirmed"
               :backendConfirmedUrl="backendConfirmedUrl"/>
    <ConnectBackend v-if="!backendConfirmed"
                    v-on:confirmBackend="confirmBackend"/>
    <MainContent v-if="backendConfirmed"/>
  </div>

</template>

<script>
import ConnectBackend from './components/ConnectBackend.vue';
import LeftPanel from './components/LeftPanel.vue';
import MainContent from './components/MainContent.vue';

export default {
  name: 'App',
  components: {
    ConnectBackend,
    LeftPanel,
    MainContent
  },
  methods: {
    confirmBackend: function (backendUrl) {
      console.log("YES: ", backendUrl)
      this.backendConfirmed = true;
      this.backendConfirmedUrl = backendUrl;
    }
  },
  data() {
    return {
      backendConfirmed: false,
      backendConfirmedUrl: ''
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

#mainDiv {
  display: flex;
}
</style>
