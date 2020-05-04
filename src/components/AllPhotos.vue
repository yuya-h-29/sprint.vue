<template>
  <div v-if="all" class="container"><p>this is all photo</p></div>
</template>

<script>
export default {
  name: "AllPhotos",
  data: () => {
    all: true;
  },
};
</script>

<style scoped>
.container {
  background-color: rgb(190, 190, 190);
}
</style>
