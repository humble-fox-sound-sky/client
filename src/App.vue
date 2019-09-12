<template>
  <div class="w-full h-screen" id="main-bg">
    <button2 @apa="fetchData()"></button2>
    <Header></Header>
    <Content :songs="songs"></Content>
    <footer class="border-2 border-transparent rounded-full">
      <div class="text-xs text-right mr-2">
        <i class="far fa-copyright"></i> 2019, Soundsky
      </div>
    </footer>
  </div>
</template>

<script>
import Header from './Header';
import Content from './Content'
import axios from 'axios';
import button2 from './buttonAdd'
export default {
    components : {
        Header,
        Content,
        button2
    },
    created (){
        this.fetchData()
    },
    data (){
      return {
        songs : []
      }
    },
    methods : {
        fetchData (){
            axios.get('http://localhost:3000/post')
            .then(({data})=>{
                this.songs = data
            })
            .catch(console.log)
        },
        masuk (data){
          this.songs.unshift(data)
        }
    }
};
</script>

<style>
</style>