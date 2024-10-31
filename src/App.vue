<script setup lang="ts">
import { h, ref } from 'vue';
import Comp from './Comp.vue';

const foo = ref<string>('foo');

/* BUG 1 */

// val should be of type 'string', not 'unknown'
const FunctionalComponent = () => h(Comp, {
  /* unknown */ modelValue: foo.value, 
  ['onUpdate:modelValue']: (val /* unknown */) => foo.value = val,
});
</script>

<template>

  <!-- BUG 2 -->
   
  <Comp/> <!-- this errors as expected -->
  <Comp :whatever="''" /> <!-- but somehow passing *any* prop makes the model value not required? -->
  
</template>
