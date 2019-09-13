<template>
  <div>
    <div class="w-full h-screen" id="main-bg">
      <button2 @apa="fetchData()"></button2>
      <Header></Header>
      <Content :songs="songs"></Content>
    </div>
    <footer class="border-2 border-transparent rounded-full flex justify-between">
      <FBshare></FBshare>
      <div class="text-xs text-right mr-2 inline-block flex items-center">
        <i class="far fa-copyright"></i> 2019, Soundsky
      </div>
    </footer>
  </div>
</template>

<script>
import axios from "axios";
import Header from "./Header";
import Content from "./Content";
import button2 from "./buttonAdd";
import FBshare from "./FBShareButton";
export default {
  components: {
    Header,
    Content,
    button2,
    FBshare
  },
  created() {
    this.fetchData();
  },
  data() {
    return {
      songs: []
    };
  },
  methods: {
    fetchData() {
      axios
        .get("http://35.234.104.53/post")
        .then(({ data }) => {
          console.log(data.data[0]);
          this.songs = data.data;
        })
        .catch(console.log);
    },
    masuk(data) {
      this.songs.unshift(data);
    }
  }
};
</script>

<style>
</style>