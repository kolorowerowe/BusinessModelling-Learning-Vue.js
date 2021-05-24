<template>
  <div>
    <h3>File</h3>

    <input type="file" @change="previewFile" accept="*.csv">

    <h3>Columns</h3>

    <label>
      Provide columns separated by comma
      <input v-model="columns"
             placeholder="Enter back-end URL" class="input">
    </label>


    <p>
      Your columns:
    </p>
    <ol>
      <li v-for="col in columnsList" :key="col">
        {{ col }}
      </li>
    </ol>


    <h3>Confirm</h3>

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
  props: {
    columnsConfirmed: String
  },
  data() {
    return {
      fileData: '',
      columns: this.columnsConfirmed
    }
  },
  computed: {
    columnsList() {
      return this.columns.split(',')
    }
  },
  methods: {
    previewFile(event) {
      const file = event.target.files[0];
      if (file) {
        const reader = new FileReader()
        reader.addEventListener('load', (event) => {
          this.fileData = event.target.result;
        })
        reader.readAsText(file);
      } else {
        console.log('No file provided')
      }

    },
    confirmFile: function () {
      if (!this.fileData) {
        alert('Please, specify the file');
        return;
      }
      if (!this.columns.length) {
        alert('No columns specified');
        return;
      }

      this.$emit('confirmFile', this.fileData, this.columns)

    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

h3 {
  margin-top: 30px;
  margin-bottom: 10px;
}

ol {
  padding-left: 50px;
}

</style>
