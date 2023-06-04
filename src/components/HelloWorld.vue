<script setup lang="ts" generic="T">
import {defineModel, watchEffect} from "vue";
import type {GroupedType} from "@/GroupedType";

defineSlots<{
  default?: (props: { message: string }) => any
}>();

const { msg = 'Default Message' } = defineProps<{
  msg: string,
  grouped: GroupedType<T>
}>();

const modelValue = defineModel({ default: 'Super Title'});

watchEffect(() => {
  console.log(msg);
});
</script>

<template>
  <slot
    :message="msg"
  />

  <template
    v-for="groupedItem in grouped.grouped"
  >
    <h1
      v-text="groupedItem"
    />
  </template>

  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <input type="text" v-model="modelValue">
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
