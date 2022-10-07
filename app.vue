<script setup lang="ts">

import { Gender, Popularity, Length } from './data';

// buttonList use to render buttons
const buttonList: { gender: Gender[], popularity: Popularity[], length: Length[] } = {
    gender: [],
    popularity: [],
    length: []
};

buttonList.gender = Object.keys(Gender).map(key => Gender[key]);
buttonList.popularity = Object.keys(Popularity).map(key => Popularity[key]);
buttonList.length = Object.keys(Length).map(key => Length[key]);

// to store current active button
const option = ref({
    gender: Gender.BOY,
    popularity: Popularity.TRENDY,
    length: Length.SHORT
});

const selectedNames = ref<string[]>([]);

const removeName = (index: number) => {
    selectedNames.value.splice(index, 1);
}

</script>

<template>

    <div class="text-center p-20">
        <h1 class="text-red-400 text-8xl my-10">Name Generator</h1>
        <ButtonGroup :selected-names="selectedNames" :option="option" :button-list="buttonList" />
        <NamesList :selected-names="selectedNames" @click="(index: number) => removeName(index)" />
    </div>

</template>

<style lang="postcss" scope>

</style>
