<template>
  <div id="mainContent">
    <h3>Here is your process</h3>
    <img v-if="imageReady" v-bind:src="imageBase64Data" alt="Business model" id="model_img">
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: 'MainContent',
  data() {
    return {
      imageBase64Data: undefined,
      imageReady: false
    }
  },
  props: {
    backendConfirmedUrl: String
  },
  methods: {
    fetchImage() {
      if (this.backendConfirmedUrl) {

        var bodyFormdata = new FormData();

        var content = 'Case ID,Activity,Start Timestamp\n' +
            '1,a,19.04.21 15:10\n' +
            '1,a,19.04.21 15:11\n' +
            '1,b,19.04.21 15:12\n' +
            '1,c,19.04.21 15:13\n' +
            '1,c,19.04.21 15:14\n' +
            '1,d,19.04.21 15:15\n' +
            '1,e,19.04.21 15:16\n' +
            '1,g,19.04.21 15:17\n' +
            '2,a,19.04.21 15:10\n' +
            '2,b,19.04.21 15:11\n' +
            '2,c,19.04.21 15:12\n' +
            '2,d,19.04.21 15:13\n' +
            '2,f,19.04.21 15:14\n' +
            '2,g,19.04.21 15:15\n' +
            '3,a,19.04.21 15:10\n' +
            '3,c,19.04.21 15:11\n' +
            '3,b,19.04.21 15:12\n' +
            '3,d,19.04.21 15:13\n' +
            '3,e,19.04.21 15:14\n' +
            '3,e,19.04.21 15:15\n' +
            '3,g,19.04.21 15:16\n' +
            '4,a,19.04.21 15:10\n' +
            '4,c,19.04.21 15:11\n' +
            '4,b,19.04.21 15:12\n' +
            '4,d,19.04.21 15:13\n' +
            '4,f,19.04.21 15:14\n' +
            '4,g,19.04.21 15:15\n' +
            '5,a,19.04.21 15:10\n' +
            '5,a,19.04.21 15:11\n' +
            '5,b,19.04.21 15:12\n' +
            '5,c,19.04.21 15:13\n' +
            '5,d,19.04.21 15:14\n' +
            '5,e,19.04.21 15:15\n' +
            '5,e,19.04.21 15:16\n' +
            '5,g,19.04.21 15:17\n' +
            '6,a,19.04.21 15:10\n' +
            '6,a,19.04.21 15:11\n' +
            '6,a,19.04.21 15:12\n' +
            '6,b,19.04.21 15:13\n' +
            '6,c,19.04.21 15:14\n' +
            '6,d,19.04.21 15:15\n' +
            '6,f,19.04.21 15:16\n' +
            '6,g,19.04.21 15:17\n' +
            '7,a,19.04.21 15:10\n' +
            '7,c,19.04.21 15:11\n' +
            '7,c,19.04.21 15:12\n' +
            '7,b,19.04.21 15:13\n' +
            '7,d,19.04.21 15:14\n' +
            '7,e,19.04.21 15:15\n' +
            '7,e,19.04.21 15:16\n' +
            '7,g,19.04.21 15:17\n' +
            '8,a,19.04.21 15:10\n' +
            '8,c,19.04.21 15:11\n' +
            '8,c,19.04.21 15:12\n' +
            '8,c,19.04.21 15:13\n' +
            '8,b,19.04.21 15:14\n' +
            '8,d,19.04.21 15:15\n' +
            '8,f,19.04.21 15:16\n' +
            '8,g,19.04.21 15:17\n'; // the body of the new file...
        var blob = new Blob([content], {type: "text/csv"});

        bodyFormdata.append('file', blob)
        bodyFormdata.append('columns', 'Case ID,Activity,Start Timestamp')
        bodyFormdata.append('min_node_value', 9)

        axios
            .post(`${this.backendConfirmedUrl}/image`, bodyFormdata,
                {responseType: 'arraybuffer'}
            )
            .then(response => {
              let returnedB64 = Buffer.from(response.data).toString('base64');
              this.imageBase64Data = `data:image/png;base64, ${returnedB64}`;
              this.imageReady = true;
            })
      }
    }
  },
  mounted() {
    this.fetchImage();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#mainContent {
  margin-left: 400px;
}
#model_img {
  margin-left: auto;
  margin-right: auto;
  display: block;
}
</style>
