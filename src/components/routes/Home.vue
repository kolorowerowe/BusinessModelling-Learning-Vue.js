<template>
  <h1>Welcome to Business Modeling App</h1>

  <p>
    Here you can visualise your business process.
  </p>

  <h3>
    Run your backend
  </h3>
  <p>
    - Backend can be attached with your application or you can use notebook from this
    <a href="https://colab.research.google.com/drive/1GHZnDvE6TSVsZWcQdw5eVA_rvh4vubkO?usp=sharing">link</a>
  </p>
  <p>
    - Run all the cell from notebook, it is supposed to keep running the last cell, don't stop the process.
  </p>
  <p>
    - Go to 'backend' tab in this application. Provide backend URL from the log of the last running cell. It should look
    like http://82f2a61fb49a.ngrok.io/
  </p>
  <p>
    - Click connect to backend. If something will be wrong, you will see the message.
  </p>


  <h3>
    Select file
  </h3>
  <p>
    - Go to the File tab. Select your csv file. You can specify here custom header columns.
  </p>
  <p>
    - If everything will be ok, you can click Confirm File
  </p>


  <h3>
    View your data
  </h3>
  <p>
    - Go to the Chart tab. If no backend was provided or no file was chosen the appropriate message will appear.
  </p>
  <p>
    - If everything will be ok, you should see the image of your business model.
  </p>
  <p>
    - You can filter, only by minimum node value. When you change the value, the image should automatically rerender.
  </p>

  <h3>
    Any comments
  </h3>
  <p>
    If you have any comments about the app you can contact me on mail: <a href="mailto:dominos55555@gmail.com">dominos55555@gmail.com</a>
  </p>

</template>

<script>
export default {
  name: "Home"
}
</script>

<style scoped>
h3 {
  margin-top: 30px;
  margin-bottom: 10px;
}
</style>