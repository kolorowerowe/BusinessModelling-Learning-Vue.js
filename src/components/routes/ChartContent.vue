<template>
  <div>


    <h3>
      Filters
    </h3>
    <label>
      Min node value
      <input v-model="minNodeValue" placeholder="0" class="input" type="number" id="minNodeValueFilter">
    </label>


    <div class="div-inline">
      <h3>Here is your process</h3>
    </div>

    <Alert v-if="!backendConfirmedUrl" msg="Connect to the backend first!" severity="warning"></Alert>
    <Alert v-if="!fileData" msg="Please select csv file to process." severity="warning"></Alert>

    <Alert v-if="!!error" :msg="error.message" severity="error"></Alert>

    <p v-if="loading">
      Loading...
    </p>

    <img v-if="!loading && !error && !!imageBase64Data" v-bind:src="imageBase64Data" alt="Business model" id="model_img">
  </div>
</template>

<script>
import axios from "axios";
import Alert from "../generic/Alert";

export default {
  name: 'ChartContent',
  components: {Alert},
  data() {
    return {
      imageBase64Data: undefined,
      minNodeValue: 0,
      loading: false,
      error: null
    }
  },
  props: {
    backendConfirmedUrl: String,
    fileData: String,
    columnsConfirmed: String,
  },
  methods: {
    fetchImage() {
      this.error = null;
      if (this.backendConfirmedUrl) {

        this.loading = true;

        var bodyFormdata = new FormData();


        var blob = new Blob([this.fileData], {type: "text/csv"});


        bodyFormdata.append('file', blob)
        bodyFormdata.append('columns', this.columnsConfirmed)
        bodyFormdata.append('min_node_value', this.minNodeValue ? this.minNodeValue : 0)

        axios
            .post(`${this.backendConfirmedUrl}/image`, bodyFormdata,
                {responseType: 'arraybuffer'}
            )
            .then(response => {
              let returnedB64 = Buffer.from(response.data).toString('base64');
              this.imageBase64Data = `data:image/png;base64, ${returnedB64}`;
            })
            .catch(err => {
              this.error = err;
            })
            .finally(() => {
              this.loading = false;
            })
      }
    }
  },
  mounted() {
    this.fetchImage();
  },
  watch: {
    minNodeValue: function () {
      this.fetchImage();
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


#model_img {
  margin-left: auto;
  margin-right: auto;
  display: block;
}
</style>
