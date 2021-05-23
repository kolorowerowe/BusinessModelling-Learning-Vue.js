<template>
  <div id="leftPanel">
    <h1>
      B M A
    </h1>

    <div v-for="element in sideBarElements"
         :key="element.value"
         @click="() => setRoute(element.value)"
         class="sideBarElement"
         v-bind:class="{'sideBarElement': true, 'sideBarElementActive': (route===element.value)}">
      <h3>
        {{ element.primary }}
      </h3>
      <v-icon v-if="element.warning" color="white">
        mdi-alert
      </v-icon>
    </div>


    <!--    <h3>-->
    <!--      Backend-->
    <!--    </h3>-->
    <!--    <p v-if="!backendConfirmed">Not confirmed</p>-->
    <!--    <div v-else class="div-inline">-->
    <!--      <p>URL: {{ backendConfirmedUrl }}</p>-->
    <!--      <v-btn @click="editBackend" icon color="white" small>-->
    <!--        <v-icon>-->
    <!--          mdi-backspace-outline-->
    <!--        </v-icon>-->
    <!--      </v-btn>-->
    <!--    </div>-->

    <!--    <h3>-->
    <!--      File-->
    <!--    </h3>-->
    <!--    <p v-if="!fileConfirmed">Not confirmed</p>-->
    <!--    <div v-else class="div-inline">-->
    <!--      <p>Confirmed</p>-->
    <!--      <v-btn @click="editFile" icon color="white" small>-->
    <!--        <v-icon>-->
    <!--          mdi-backspace-outline-->
    <!--        </v-icon>-->
    <!--      </v-btn>-->
    <!--    </div>-->


  </div>
</template>

<script>
export default {
  name: 'LeftPanel',
  props: {
    backendConfirmed: Boolean,
    backendConfirmedUrl: String,
    fileConfirmed: Boolean,
    route: String
  },
  computed: {
    sideBarElements(){
      return [
        {
          primary: 'Home',
          value: 'HOME',
          warning: false
        },
        {
          primary: 'Backend',
          value: 'BACKEND',
          warning: !this.backendConfirmed
        },
        {
          primary: 'File',
          value: 'FILE',
          warning: !this.fileConfirmed
        },
        {
          primary: 'Chart',
          value: 'CHART',
          warning: false
        }
      ]
    }
  },
  data() {
    return {
    }
  },
  methods: {
    editBackend() {
      this.$emit('editBackend')
    },
    editFile() {
      this.$emit('editFile')
    },
    setRoute(newRoute) {
      this.$emit('setRoute', newRoute)
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
  width: 230px;
  position: fixed;
  z-index: 1;
  top: 0;
  left: 0;
}

#leftPanel > h1 {
  color: #34495E;
  font-weight: 900;
  font-size: 60px;
  padding: 10px 10px 50px 10px;
}

#minNodeValueFilter {
  min-width: 30px;
  max-width: 100px;
}

.sideBarElement {
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 15px;
}

.sideBarElementActive {
  background-color: #34495E;
}
</style>
