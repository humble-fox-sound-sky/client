<template>
  <div>
    <div class="fixed w-full" >
      <div class="flex w-full">
        <button class="text-4xl text-orange-600" @click="showModal(true)">
          <i class="fas fa-music p-5"></i>
        </button>
      </div>
    </div>
    <div class="modal-mask" v-if="kondisi">
      <div
        class="h-screen bg-transparent fixed w-full flex items-center justify-center z-50 border-gray-200"
      >
        <div class="bg-white fixed w-64 border-2 border-yellow-600 p-5 rounded shadow-lg">
          <form enctype="multipart/form-data" @submit.prevent="addPost">
            <div class="mb-2">
              <label for="name">Nickname:</label>
              <input type="text" id="name" class="px-4 py-1 border-2 border-gray-100 rounded-b" v-model="name" />
            </div>
            <div class="mb-2">
              <label for="mood">Your mood:</label>
              <input type="text" id="mood" class="px-4 py-1 border-2 border-gray-100 rounded-b" v-model="description" />
            </div>
            <div class="flex justify-between items-center px-5 mt-4">
              <input type="file"  @change="previewFile" id="file" ref="myFiles">
              <input type="submit" class="bg-orange-500 px-2 py-1 rounded-full" value="submit">
                <!-- <i class="fas fa-cloud-upload-alt text-4xl text-orange-600"></i> -->
                <button @click="showModal(false)">Close</button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
    data (){
        return {
            kondisi : false,
            name : '',
            description : '',
            music : ''
        }
    },
    methods : {
        showModal(kondisi){
            this.kondisi = kondisi
        },
        addPost (){
            let { name , description ,  music } = this
            var bodyFormData = new FormData();
            console.log(music[0] , music , '.,.,.,.,.,.,.<<<<')
            bodyFormData.append('audio', music[0]); 
            bodyFormData.append('name' ,  name)
            bodyFormData.append('description' , description)
            console.log(bodyFormData , ' check')
            axios({
                method : 'POST',
                url : 'http://localhost:3000/post',
                data : bodyFormData
            })
            .then(({data})=>{
                this.kondisi = false
                this.$emit('apa' , data)
                console.log(data , ' ,,,,,,,,,,,,,,,,,,,,,,')
            })
            .catch(console.log)
        },
        previewFile(){
            this.music = this.$refs.myFiles.files
        }
    }
};
</script>

<style>
</style>