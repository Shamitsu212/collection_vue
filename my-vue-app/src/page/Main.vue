<script setup lang="ts">

import Button_UI from '../components/UI/Button_UI.vue';
import Collection_UI from '../components/UI/Collection_UI.vue';
import Input_UI from '../components/UI/Input_UI.vue';
import {collections, type collection} from '../data';

import { ref, watch, computed } from 'vue';

const search = ref<string>("")
const selectedTag = ref<string>("Все")

const filteredCollections = computed<collection[]>(() => {
  
    return collections.filter(item => {

        const calcTag = selectedTag.value === "Все" || item.tag.toLowerCase() === selectedTag.value.toLowerCase()
        const calcSearch = search.value === "" || item.label.toLowerCase().includes(search.value.toLowerCase())

        return calcTag && calcSearch
  })
})

const itemsInPage:number = 4;
const setPage = ref<number>(1)

const totalPages = computed(() => {
    return Math.ceil(filteredCollections.value.length / itemsInPage)
}) 

const paginetedCollections = computed(() => {
    const startIndex = (setPage.value - 1) * itemsInPage
    return filteredCollections.value.slice(
      startIndex,
      startIndex + itemsInPage
    )
})

const buttonsArr = computed(() =>
  Array.from({ length: totalPages.value }, (_, i) => i + 1)
)

watch([search, selectedTag], () => {
  setPage.value = 1
})


</script>

<template>

  <div class="Page">

    <div class="Page__buttonContainer">

        <Button_UI text="Все"  :activeTag="selectedTag" @select="selectedTag = $event"/>
        <Button_UI text="Море" :activeTag="selectedTag" @select="selectedTag = $event"/>
        <Button_UI text="Горы" :activeTag="selectedTag" @select="selectedTag = $event"/>
        <Button_UI text="Архитектура" :activeTag="selectedTag" @select="selectedTag = $event"/>
        
        <Input_UI v-model="search"/>

    </div>

    <div class="Page__Map">
        <Collection_UI v-for="c in paginetedCollections" :collection="c"/>
    </div>

    <div class="Page__buttonContainer">

        <button v-for="b in buttonsArr" :key="b" @click="setPage = b" class="Button">
            {{ b }}
        </button>

    </div>

  </div>

</template>

<style scoped>
.Page{
    width: 1920px;
    height: 1080px;

    padding-bottom: 60px;
    padding-top: 40px;

    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 40px;
}
.Page__buttonContainer{
    display: flex;
    flex-direction: row;
    gap: 10px;
}
.Page__Map{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    row-gap: 10px;
    column-gap: 20px;

    width: 1200px;
    height: auto;
}
</style>
