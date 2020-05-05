<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
    <h1>{{ func1() }}</h1>

    <navbar />
    <allPhotos />
    <!-- this is how diplay pictures -->
    <div v-for="photo in this.photos" :key="photo.id">
      <img :src="photo.url" class="pic" />
    </div>

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

      // console.log(changeToBase64)

      for (let i = 0; i < changeToBase64.length; i++){
        this.photos.push({id:i, url:changeToBase64[i]})
      }
      // this.photos = [...changeToBase64];
      // console.log(this.photos);
      // this.photo.concat(changeToBase64)
      // return this.photos;
    },
  },
};
</script>

<style scoped>
#app {
  text-align: center;
}
.pic {
  width: 100px;
  height: 100px;
}
</style>
