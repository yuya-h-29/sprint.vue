<template>
  <div>
    <p>{{ title }}</p>
    <input type="file" name="upload" />
  </div>
</template>

<script>
export default {
  name: "Upload",
  data: () => ({
    title: "this is from upload",
  }),
};
</script>

<style></style>
