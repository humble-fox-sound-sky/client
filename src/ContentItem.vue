<template>
  <div>
    <div
      class="h-24 h-12 border-transparent border-2 shadow flex"
    >
      <div class="w-1/2 p-4">
        <h3>{{song.name}}</h3>
        <p class="text-sm">Hey check this out!</p>
      </div>
      <div class="w-1/2 flex justify-center items-center">
        <audio controls class="h-6 w-64">
          <source :src="song.url" />
        </audio>
      </div>
    </div>
  </div>
</template>

<script>
export default {
    props : ["song"]
};
</script>

<style>
</style>