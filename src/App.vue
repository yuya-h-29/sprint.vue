<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
    <!-- <img ：src="photos" alt="" srcset="" /> -->
    <!-- <h1>{{ func1() }}</h1> -->
    <!-- <h1>{{ photos }}</h1> -->
    <!-- <div v-for="n in 100" :key="item.message"> -->
    <!-- <img src="" alt="" srcset=""> -->
    <!-- </div> -->
    <navbar />
    <allPhotos />
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
    photos: [],
    currentView: "all",
    selectedPhoto: "none",
  }),
  methods: {
    func1: async function getAllPictures() {
      const arrOfPromisePictures = await listObjects();
      // console.log(arrOfPromisePictures);
      const arrOrPicFiles = arrOfPromisePictures.map((obj) => {
        return obj.Key;
      });
      const changeToBase64 = Promise.all(
        arrOrPicFiles.map((fileName) => {
          return getSingleObject(fileName);
        })
      ).then((result) => {
        result.map((pictureData) => {
          return "data:image/jpg;base64," + pictureData;
        });
      });
      return this.photos.push(changeToBase64);
    },
  },
};
</script>

<style>
#app {
  text-align: center;
}
</style>
