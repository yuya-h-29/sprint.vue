<template>
  <div class="nav">
    <button class="home" v-on:click="home">Home</button>
    <upload />
  </div>
</template>

<script>
import Upload from "./Upload";

export default {
  name: "Navbar",
  components: {
    upload: Upload,
  },
  methods: {
    home: function () {
      alert("hi");
    },
  },
};
</script>

<style scoped>
.nav {
  background-color: rgb(143, 173, 143);
  display: flex;
  justify-content: flex-end;
}

.home {
  padding: 20px;
  margin-right: auto;
}
</style>
