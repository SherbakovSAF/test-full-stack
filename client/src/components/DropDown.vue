<script lang="ts">
import CheckedIcon from './icons/CheckedIcon.vue';
import ChevronIcon from './icons/ChevronIcon.vue'
import {defineComponent, ref, onMounted } from 'vue'
import type {Ref} from 'vue'

import { TypeOption } from '@/interfaces'

export default defineComponent({
  components: {CheckedIcon, ChevronIcon},
  
  setup(props, {emit}) {
    const types: Ref<TypeOption[]> = ref([
    { id: 0, title: 'Не выбрано', url: null},
    { id: 1, title: 'Сделка', url: 'leads'},
    { id: 2, title: 'Контакт', url: 'contacts'},
    { id: 3, title: 'Компания', url: 'companies'},
    ]);
    const currentType: Ref<TypeOption> = ref(types.value[0])

    function emitChangeSelectType():void{
      emit('changeSelectType', currentType.value)
    }

    function switchTypeSelect(type: TypeOption):void{
      if(currentType.value == type) return
      currentType.value = type;
      emitChangeSelectType()
    }

    onMounted(()=> {
      emitChangeSelectType()
    })
    
  return {
      currentType,
      types,
      switchTypeSelect
    }
}
})

</script>

<template>
  <div id="select">
    <label>
      <div id="current-type">
        <p>{{ currentType.title }}</p>
        <ChevronIcon />
      </div>
      <input id="select-toggle" type="checkbox">
    </label>
    <ul id="drop-down">
      <li v-for="(type) in types" :key="type.id" 
        @click="switchTypeSelect(type)">

        <CheckedIcon v-show="currentType.id == type.id" hex-color="grey"/>
        <p>{{type.title}}</p>

      </li>
    </ul>
  </div>
</template>

<style scoped>
#select{
  width: 400px;
  position: relative;
}

#select:has(#select-toggle:checked) > #drop-down{
  display: block;
}

#select:has(#select-toggle:checked) #current-type > i{
  rotate: 180deg;
}

#select-toggle{
  display: none;
}

#current-type {
  width: 100%;
  display: flex;
  justify-content: space-between;
  border: 1px solid var(--text-color);
  padding: 0.5em 1em;
  border-radius: 5px;
  cursor: pointer;
}

#drop-down {
  position: absolute;
  top: calc(100% + 20px);
  left: 0;
  z-index: 1;
  border-radius: 5px;
  width: 100%;
  border: 1px solid var(--text-color); /* Переменные в base.css */
  list-style: none;
  display: none;
}

#drop-down > li{
  display: flex;
  align-items: center;
  cursor: pointer;
  padding: 0.5em 1em;
}

#drop-down > li:hover{
  background-color: rgb(231, 231, 231);
}
</style>
