<template>
  <div id="mainContent">
    <div class="div-inline">
      <h3>Here is your process</h3>
      <v-btn @click="onRefresh" icon color="white" small>
        <v-icon>
          mdi-backspace-outline
        </v-icon>
      </v-btn>
    </div>
    <v-progress-circular
        v-if="loading"
        :size="50"
        color="#34495E"
        indeterminate
    ></v-progress-circular>
    <img v-if="!loading && !!imageBase64Data" v-bind:src="imageBase64Data" alt="Business model" id="model_img">
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'MainContent',
  data() {
    return {
      imageBase64Data: undefined,
      loading: false
    }
  },
  props: {
    backendConfirmedUrl: String,
    fileData: String,
    columns: [String],
    minNodeValue: Number
  },
  methods: {
    onRefresh() {

    },
    fetchImage() {
      if (this.backendConfirmedUrl) {

        this.loading = true;

        var bodyFormdata = new FormData();


        var blob = new Blob([this.fileData], {type: "text/csv"});


        bodyFormdata.append('file', blob)
        bodyFormdata.append('columns', this.columns.join(','))
        bodyFormdata.append('min_node_value', this.minNodeValue)

        axios
            .post(`${this.backendConfirmedUrl}/image`, bodyFormdata,
                {responseType: 'arraybuffer'}
            )
            .then(response => {
              let returnedB64 = Buffer.from(response.data).toString('base64');
              this.imageBase64Data = `data:image/png;base64, ${returnedB64}`;
              this.imageReady = true;
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
#mainContent {
  margin-left: 300px;
}

#model_img {
  margin-left: auto;
  margin-right: auto;
  display: block;
}
</style>
