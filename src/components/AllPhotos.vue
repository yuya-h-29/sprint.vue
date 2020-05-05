<template>
  <div class="container">
    <img :src="photo.url" class="pic" />
  </div>
</template>

<script>
export default {
  name: "AllPhotos",
  props: ["photo"],
  // data: () => {
  //   all: true;
  // },
};
</script>

<style scoped>
.container {
  background-color: rgb(190, 190, 190);
}
.pic {
  width: 100px;
  height: 100px;
}
</style>
