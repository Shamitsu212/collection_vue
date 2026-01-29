<script setup lang="ts">

const props = defineProps <{
    text: string;
    activeTag: string;
}>()

const emits = defineEmits<{
    (e: `select`, value: string):void
}>()

function handleClick() {
    emits('select', props.text)
}

</script>

<template>

    <button 
        class="Button"
        @click="handleClick"
        :disabled="text == activeTag"
    >
        {{ text }}
    </button>
  
</template>

<style>
.Button{
    background-color: white;

    color: black;
    font-size: 16px;
    font-weight: bold;

    min-width: 40px;
    min-height: 30px;

    padding: 5px;
    
    border: none;
    border-radius: 12px;
}
.Button:hover{
    background-color: black;
    color: white;
}
.Button:disabled{
    background-color: black;
    color: white;
}
</style>
