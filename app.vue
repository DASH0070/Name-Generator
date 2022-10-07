<script setup lang="ts">

import { Gender, Popularity, Length, names } from './data';

// enum Gender {
//     GIRL = 'Girl',
//     BOY = 'Boy',
//     UNISEX = 'Unisex'
// }

// enum Length {
//     LONG = 'Long',
//     SHORT = 'Short',
//     ALL = 'All'
// }

// enum Popularity {
//     TRENDY = 'Trendy',
//     UNIQUE = 'Unique'
// }

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

// apply class based on current option
const checkClass = (elem: string[], key: string, btn: string, index: number) => {
    let str = '';
    if (index === 0)
        str += ' rounded-l-full ';
    if (index === elem.length - 1)
        str += ' rounded-r-full ';
    if (btn === option.value[key])
        str += ' text-white bg-red-400 ';
    else
        str += ' text-indigo-400 '
    return str;
}

// Change value of option if btn clicked
const btnClick = (e: MouseEvent, key: string) => {
    const target = e.target as HTMLElement;
    option.value[key] = target.innerText;
    return e;
}

const selectedNames = ref<string[]>([]);
const generateNames = (e: MouseEvent) => {
    selectedNames.value = [];
    for (let i = 0; i < names.length; i++) {
        if (names[i].gender === option.value.gender &&
            (option.value.length === Length.ALL || names[i].length === option.value.length) &&
            names[i].popularity === option.value.popularity)
            selectedNames.value.push(names[i].name);
    }
    return e;
}

</script>

<template>

    <div class="text-center p-20">
        <h1 class="text-red-400 text-8xl my-10">Name Generator</h1>
        <div class="bg-red-100 rounded-[3rem] w-[60rem] mx-auto py-20 ">
            <div v-for="(elem, key) in buttonList" class="option-container my-8" :key="key">
                <button v-for="(btn, index) in elem" :key="index"
                    class="text-2xl w-32 h-14 border-2 border-red-400 outline-none "
                    :class="checkClass(elem, key, btn, index)" @click="(e: MouseEvent) => btnClick(e, key)">
                    {{btn}}
                </button>
            </div>
            <button @click="(e: MouseEvent) => generateNames(e)"
                class="bg-red-700 text-white w-52 h-12 rounded-full mt-12 text-xl tracking-wide uppercase">Generate
                Names</button>
        </div>
        <ul class="flex justify-center gap-8 flex-wrap my-8">
            <li class="text-red-400 text-xl" v-for="names in selectedNames" :key="names">{{names}}</li>
        </ul>
    </div>

</template>

<style lang="postcss" scope>

</style>
