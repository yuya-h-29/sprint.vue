<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <h1>{{}}</h1>

    <navbar />
    <allPhotos />
    <singlePhoto />
  </div>
</template>

<script>
import Navbar from "./components/Navbar";
import AllPhotos from "./components/AllPhotos";
import SinglePhoto from "./components/SinglePhoto";
import { listObjects} from "../utils/index";

//  getSingleObject, saveObject

export default {
  name: "App",
  components: {
    navbar: Navbar,
    allPhotos: AllPhotos,
    singlePhoto: SinglePhoto,
  },
  data: () => ({
    photo: [],
  }),
  methods: {
      func1:function name(params) {

      },
  //     selectOnePhoto(el) {
  // console.log("something else")
  //     }


  //
  //   }
};
</script>

<style>
#app {
  text-align: center;
}
</style>
