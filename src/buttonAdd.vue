<template>
  <div>
    <div class="fixed w-full">
      <div class="flex w-full">
        <button class="text-4xl focus:outline-none button pumpkin" @click="showModal(true)">
          <i class="fas fa-music p-5"></i>
        </button>
      </div>
    </div>
    <transition name="modal">
      <div class="modal-mask" v-if="kondisi">
        <div
          class="h-screen bg-transparent fixed w-full flex items-center justify-center z-50 border-gray-200 modal-container"
        >
          <div class="bg-white fixed w-1/4 border-4 border-yellow-600 p-5 rounded shadow-lg">
            <form enctype="multipart/form-data" @submit.prevent="addPost">
              <div class="mb-2">
                <label for="name">Nickname:</label>
                <br />
                <input
                  type="text"
                  id="name"
                  class="px-4 py-1 w-full border-2 border-gray-100 rounded-b"
                  v-model="name"
                />
              </div>
              <div class="mb-2">
                <label for="mood">Your mood:</label>
                <br />
                <input
                  type="text"
                  id="mood"
                  class="px-4 py-1 w-full border-2 border-gray-100 rounded-b"
                  v-model="description"
                />
              </div>
              <div class="mt-4">
                <input
                  class="w-full focus:outline-none"
                  type="file"
                  @change="previewFile"
                  id="file"
                  ref="myFiles"
                />
                <div class="flex w-full justify-around">
                  <div>
                    <input
                      type="submit"
                      class="bg-orange-500 px-2 py-1 rounded-full mt-4 focus:outline-none"
                      value="submit"
                      id="upload"
                    />
                  </div>
                  <!-- <i class="fas fa-cloud-upload-alt text-4xl text-orange-600"></i> -->
                  <div>
                    <button
                      class="bg-red-500 px-2 py-1 rounded-full mt-4 focus:outline-none"
                      @click="showModal(false)"
                    >cancel</button>
                  </div>
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      kondisi: false,
      name: "",
      description: "",
      music: ""
    };
  },
  methods: {
    showModal(kondisi) {
      this.kondisi = kondisi;
    },
    addPost() {
      let { name, description, music } = this;
      var bodyFormData = new FormData();
      console.log(music[0], music, ".,.,.,.,.,.,.<<<<");
      bodyFormData.append("audio", music[0]);
      bodyFormData.append("name", name);
      bodyFormData.append("description", description);
      console.log(bodyFormData, " check");
      axios({
        method: "POST",
        url: "https://34.87.64.243/post",
        data: bodyFormData
      })
        .then(({ data }) => {
          this.kondisi = false;
          this.$emit("apa", data);
          console.log(data, " ,,,,,,,,,,,,,,,,,,,,,,");
        })
        .catch(console.log);
    },
    previewFile() {
      this.music = this.$refs.myFiles.files;
    }
  }
};
</script>

<style>
</style>