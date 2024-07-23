<template>
  <div>
    <div class="cantainer">
      <div class="container_body">
        <label>Name : </label>
        <input type="text" v-model="userName" placeholder="Enter the name" />
        <br />
        <label>File :</label>
        <input
          type="file"
          @change="handleFileUpload"
          placeholder="upload a file"
        />
        <br />
        <button @click="submit">Submit</button>
      </div>
    </div>
    <button @click="fetchImage">fetchImage</button>
    <div v-if="imageUrl">
      <img class="imageContainer" :src="imageUrl" />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
      userName: '',
      upFile: null,
      imageUrl: '',
    };
  },

  methods: {
    submit() {
      const formData = new FormData();
      formData.append('userName', this.userName);
      formData.append('file', this.upFile);
      axios
        .post('http://localhost:5000/api/uploadFile', formData, {
          'Content-Type': 'multipart/form-data',
        })
        .then(() => {
          console.log('submit successful');
        })
        .catch((err) => {
          console.log('getting error', err);
        });
    },

    handleFileUpload(event) {
      const file = event.target.files[0];
      this.upFile = file;
      console.log('File selected:', this.upFile);
    },

    fetchImage() {
      this.imageUrl = 'http://localhost:5000/uploads/pexels-pixabay-460672.jpg';
      console.log('fetchImage is called');
    },
  },
};
</script>

<style scoped>
.cantainer {
  width: 100%;
  height: 100%;
  border: 5px;
  border-color: red;
  align-items: center;
  flex: auto;
  background-color: rgb(6, 26, 27);
}

/* .container_body {
  padding: 20px;
  margin: 10px;
} */

.imageContainer {
  width: 50%;
  height: 50%;
  border: 5px solid red;
  align-items: center;
}
</style>
