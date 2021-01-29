<template>
  <DragField
    :drag-over="dragOver"
    :dragLeave="dragLeave"
    :drop="drop"
    :wrong-file="wrongFile"
    :sendBase64="sendBase64"
    :image-sources="imageSources"
    :isDragging="isDragging"
  />
</template>

<script lang="ts">
import { defineComponent, Ref, ref } from 'vue';
import DragField from '@/components/DragField.vue';

export default defineComponent({
  name: 'App',
  components: {
    DragField,
  },
  setup() {
    const isDragging = ref(false);
    const wrongFile = ref(false);
    const imageSources: Ref<(string | ArrayBuffer | null | undefined)[]> = ref([]);
    const dragOver = () => {
      isDragging.value = true;
    };
    const dragLeave = () => {
      isDragging.value = false;
    };
    const sendBase64 = () => {
      if (imageSources.value.length) {
        const images = JSON.stringify({ ...imageSources.value });
        console.log(images);
      }
    };

    const drop = (e: DragEvent) => {
      const { files } = e.dataTransfer!;
      Array.from(files).forEach((file) => {
        if (file.type.indexOf('image/') >= 0) {
          const reader = new FileReader();
          reader.onload = (f) => {
            if (!imageSources.value.includes(f.target?.result)) {
              imageSources.value.push(f.target?.result);
              isDragging.value = false;
            }
          };
          reader.readAsDataURL(file);
        } else {
          wrongFile.value = true;
        }
      });
      isDragging.value = false;
    };

    return {
      isDragging,
      wrongFile,
      imageSources,
      dragOver,
      drop,
      dragLeave,
      sendBase64,
    };
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display:flex;
  flex-direction: column;
  justify-content: space-evenly;
}
</style>
