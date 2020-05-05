<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
    <!-- <h1>{{ func1() }}</h1> -->

    <div v-if="currentView === 'all'">
      <div v-for="photo in this.photos" :key="photo.id">
        <allPhotos :photo="photo" />
      </div>
    </div>

    

    <div v-else>
      <singlePhoto >
    </div>

    <navbar />
    <!-- this is how diplay pictures -->
    <!-- <div v-for="photo in this.photos" :key="photo.id">
      <img :src="photo.url" class="pic" />
    </div>-->

    <singlePhoto />
  </div>
</template>

<script>
import Navbar from "./components/Navbar";
import AllPhotos from "./components/AllPhotos";
import SinglePhoto from "./components/SinglePhoto";
import { listObjects, getSingleObject } from "../utils/index";

//  saveObject

export default {
  name: "App",
  components: {
    navbar: Navbar,
    allPhotos: AllPhotos,
    singlePhoto: SinglePhoto,
  },
  data: () => ({
    photos: [], //=>{{index:1,url:url1},{inde}]
    currentView: "all",
    selectedPhoto: "none",
  }),
  methods: {
    func1: async function getAllPictures() {
      const arrOfPromisePictures = await listObjects();
      const arrOrPicFiles = arrOfPromisePictures.map((obj) => {
        return obj.Key;
      });
      const getArrOfFiles = await Promise.all(
        arrOrPicFiles.map((fileName) => {
          return getSingleObject(fileName);
        })
      );
      const changeToBase64 = getArrOfFiles.map((pictureData) => {
        return "data:image/jpg;base64," + pictureData;
      });

      for (let i = 0; i < changeToBase64.length; i++){
        this.photos.push({id:i, url:changeToBase64[i]})
      }
    },
  },
};
</script>

<style scoped>
#app {
  text-align: center;
}
</style>
