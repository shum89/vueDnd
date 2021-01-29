<template>
<button type="button" class="button">
{{text}}
</button>
</template>

<script  lang="ts">

import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Button',
  props: {
    text: String,
    classModifier: String,
  },
});
</script>

<style scoped>
  .button {
    width: 168px;
    height: 36px;
    background-color: #006896;
    text-align: center;
    font: normal normal normal 16px/19px Arial;
    letter-spacing: 0;
    color: #FFFFFF;
    border: 0;
  }
</style>
