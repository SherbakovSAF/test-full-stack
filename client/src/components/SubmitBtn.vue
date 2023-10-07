<script lang="ts">
import Loader from '@/components/ui/Loader.vue'
// import ChevronIcon from './icons/ChevronIcon.vue'
import {defineComponent, ref } from 'vue'
import type {Ref} from 'vue'

import axios from 'axios'


export default defineComponent({
  components: {Loader},
  props: {
    // default нужно убрать, как компоненты начнут взаимодействовать
    sendPostType: {type: Object, required: true, default: {id: 0, title: null, url: 'loader'}}
  },
  setup(props){
    const isLoader:Ref<boolean> = ref(false)

    async function sendPost(): Promise<void>{
      try {
        isLoader.value = true;
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
  color: black;
  cursor: pointer;
}
button[type=submit]:disabled{
  background-color: #4c8bf7;
  color: white;
}
</style>
