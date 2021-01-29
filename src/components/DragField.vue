<template>
  <Preview v-if="imageSources.length > 0" :imageSources="imageSources"/>
  <div :class="['drop-field', isDragging ? 'drop-field__dragging' : '']"
       @dragover.prevent="dragOver"
       @dragleave.prevent="dragLeave"
       @drop.prevent="drop($event)">
    <h1 v-if="!isDragging">Перенесите изображение</h1>
  </div>
  <div class="drop-field__container">
    <h2 v-if="wrongFile">Неправильный формат файла</h2>
    <Button @click="sendBase64" text="Отправить"/>
  </div>
</template>

<script lang="ts">

import { defineComponent } from 'vue';
import Button from '@/components/Button.vue';
import Preview from '@/components/Preview.vue';

export default defineComponent({
  name: 'DragField',
  props: {
    isDragging: Boolean,
    wrongFile: Boolean,
    imageSources: Array,
    dragOver: Function,
    drop: Function,
    dragLeave: Function,
    sendBase64: Function,
  },
  components: {
    Button,
    Preview,
  },
});
</script>

<style scoped>
.drop-field {
  width: 100%;
  height: 250px;
  background-color: #eee;
  padding: 5rem;
  border:10px solid #eee;
  transition: background-color .2s ease-in-out;
  font-family: sans-serif;
  box-sizing: border-box;
}

.drop-field__container {
  display:flex;
  flex-direction: column;
  align-items: center;
}

.drop-field__dragging {
  background-color: #999;
}

</style>
