<script lang="ts">
import Loader from '@/components/ui/loader.vue'

import {defineComponent, ref } from 'vue'
import type {Ref} from 'vue'

import axios from 'axios'


export default defineComponent({
  components: {Loader},
  props: {
    // default нужно убрать, как компоненты начнут взаимодействовать
    sendPostType: {type: Object, required: true}
  },
  setup(props){
    const isLoader:Ref<boolean> = ref(false)
    async function sendPost(): Promise<void>{
      try {
        isLoader.value = true;
        console.log(`/api/v4/${props.sendPostType.url}`)
        await axios.post(`/api/v4/${props.sendPostType.url}`, {
          type: 'contant'
        })
      } catch (error) {
        alert(error)
      } finally {
        isLoader.value = false;
      }
    }

    return {isLoader, sendPost}
  }
})

</script>

<template>
  <button type="submit" :disabled="sendPostType.url == null" @click="sendPost">
    <Loader v-if="isLoader"/>
    <p v-else>Создать</p>
  </button>
</template>

<style scoped>
button[type=submit] {
  padding: 0.5em 1em;
  font-weight: 600;
  border: 1px solid var(--text-color);
  border-radius: 5px;
  cursor: pointer;
  background-color: #4c8bf7;
  color: white;
}
button[type=submit]:disabled{
  background-color: white;
  color: black;
}
</style>
