<script lang="ts">
import { defineComponent } from 'vue';
export default defineComponent({
    props: {
      hexColor: {type: String, required: false, default: '#000'}
    }
  })
</script>

<template>
    <i class="gg-check" :style="{color: hexColor}"></i>
</template>

<style scoped>
.gg-check {
    box-sizing: border-box;
    position: relative;
    display: block;
    transform: scale(var(--ggs,1));
    width: 22px;
    height: 22px;
    border: 2px solid transparent;
    border-radius: 100px;
}
.gg-check::after {
    content: "";
    display: block;
    box-sizing: border-box;
    position: absolute;
    left: 3px;
    top: -1px;
    width: 6px;
    height: 10px;
    border-width: 0 2px 2px 0;
    border-style: solid;
    transform-origin: bottom left;
    transform: rotate(45deg)
}
</style>