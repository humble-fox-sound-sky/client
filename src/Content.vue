<template>
  <div class="container w-2xl mx-auto">
        <div class="bg-white max-w-xl h-auto mx-auto border-4 border-transparent rounded-lg shadow-lg overflow-y-auto" id="card-list">
          <!-- ANCHOR  POST CARD -->
          <ContentItem v-for="song in songs" :key="song._id" :song="song"></ContentItem>
        </div>
    </div>
</template>

<script>
import ContentItem from './ContentItem'
export default {
  props : ["songs"],
  created(){
    console.log(this.songs , ' .,,.,<<<<<<<<<<<<<')
  },
  components: {
    ContentItem
  }
}
</script>

<style>

</style>