<template>
  <div id="leftPanel">
    <h1>
      <strong>B</strong>usiness <br>
      <strong>M</strong>odeling <br>
      <strong>A</strong>pp
    </h1>

    <h3>
      Backend
    </h3>
    <p v-if="!backendConfirmed">Not confirmed</p>
    <div v-else class="div-inline">
      <p>URL: {{ backendConfirmedUrl }}</p>
      <v-btn @click="editBackend" icon color="white" small>
        <v-icon>
          mdi-backspace-outline
        </v-icon>
      </v-btn>
    </div>

    <h3>
      File
    </h3>
    <p v-if="!fileConfirmed">Not confirmed</p>
    <div v-else class="div-inline">
      <p>Confirmed</p>
      <v-btn @click="editFile" icon color="white" small>
        <v-icon>
          mdi-backspace-outline
        </v-icon>
      </v-btn>
    </div>

    <div>
      <h3>
        Filters
      </h3>
      <label>
        Min node value
        <input v-model="minNodeValue" placeholder="0" class="input" type="number" id="minNodeValueFilter">
      </label>
      <v-btn @click="applyFilters"
             class="text-white"
             color="#34495E"
             icon
      >
        <v-icon dark right>
          mdi-check
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
    backendConfirmedUrl: String,
    fileConfirmed: Boolean,
  },
  data() {
    return {
      minNodeValue: 0
    }
  },
  methods: {
    editBackend() {
      this.$emit('editBackend')
    },
    editFile() {
      this.$emit('editFile')
    },
    applyFilters() {
      this.$emit('applyFilter', this.minNodeValue)
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
  width: 280px;
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

#minNodeValueFilter {
  min-width: 30px;
  max-width: 100px;
}
</style>
