<template>
  <div id="selectFile">
    <h3>Select your file</h3>

    <input type="file" @change="previewFile" accept="*.csv">
    <v-btn @click="confirmFile"
           class="text-white"
           color="#34495E"
    >
      Confirm file
      <v-icon dark right>
        mdi-checkbox-marked-circle
      </v-icon>
    </v-btn>
  </div>
</template>

<script>
export default {
  name: 'SelectFile',
  data() {
    return {
      fileData: '',
      columns: ['Case ID','Activity','Start Timestamp']
    }
  },
  methods: {
    previewFile(event){
      const file = event.target.files[0];
      const reader = new FileReader()
      reader.addEventListener('load', (event) => {
        this.fileData = event.target.result;
      })
      reader.readAsText(file);
      // this.fileData = file;
    },
    confirmFile: function () {
      if (this.fileData && this.columns.length) {
        this.$emit('confirmFile', this.fileData, this.columns)
      } else {
        alert('Backend URL is empty');
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#selectFile {
  margin-left: 400px;
}


</style>
