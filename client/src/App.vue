<script lang="ts">
import DropDown from '@/components/DropDown.vue';
import SubmitBtn from '@/components/SubmitBtn.vue';

import { defineComponent, ref, } from 'vue';

import { TypeOption } from '@/interfaces';

export default defineComponent({
  components: {DropDown, SubmitBtn},
  setup(){
    const typeSelect = ref({});
    function changeSelectType(e: TypeOption){
      typeSelect.value = e
    }

    return {typeSelect, changeSelectType}
  }
})

</script>

<template>
  <div id="app">
    <div id="input-panel">
      <DropDown @changeSelectType="changeSelectType"/>
      <SubmitBtn :sendPostType="typeSelect"/>
    </div>
  </div>
  
</template>

<style scoped>
#app {
  max-width: 1000px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
}

#input-panel{
  display: flex;
  grid-column-gap: 2em;
}
</style>
