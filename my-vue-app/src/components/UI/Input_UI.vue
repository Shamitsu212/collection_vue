<script setup lang="ts">

const props = defineProps<{
    modelValue: string;
}>()

const emits = defineEmits <{
    (e: 'update:modelValue', value: string):void
}>()

function onInput(event: Event) {
    const target = event.target as HTMLInputElement
    emits('update:modelValue', target.value)
}

</script>

<template>
  
  <input
    class="input"
    type="text"
    placeholder="Поиск"
    :value="modelValue"
    @input="onInput"
  >
  
</template>

<style scoped>
.input{
    background-color: white;

    border-radius: 12px;
    border: none;

    padding: 7px;
}
</style>
