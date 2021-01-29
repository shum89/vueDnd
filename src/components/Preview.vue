<template>
  <div class="image__container">
    <img class="image" v-for="(imageSource, index) in imageSources"
         :key="index" :src="imageSource" alt="Preview"/>
  </div>
</template>

<script lang='ts'>
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Preview',
  props: {
    imageSources: Array,
  },
});
</script>

<style scoped>
.image__container{
  display:grid;
  grid-auto-flow: column;
  grid-auto-columns: max-content;
  grid-gap: 10px;
  justify-content:center;
  margin-bottom: 50px;
}
.image{
  height: 250px;
  object-fit: contain;
}
</style>
