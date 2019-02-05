<template>
  <div>
    <form class="simple-form">
      <input @change="selectedFile" type="file" name="file">
      <button @click="upload" type="button">アップロード</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      uploadFile: null,
    };
  },
  methods: {
    selectedFile(e) {
      // 選択された File の情報を保存しておく
      e.preventDefault();
      const files = e.target.files;
      this.uploadFile = files[0];
    },
    upload() {
      // FormData を利用して File を POST する
      const formData = new FormData();
      formData.append('image', this.uploadFile);
      const config = {
        headers: {
          'content-type': 'multipart/form-data',
        },
      };
      axios
        .post('http://localhost:9000/upload', formData, config)
        .then((response) => {
          // response 処理
        })
        .catch((error) => {
          // error 処理
        });
    },
  },
};
</script>
