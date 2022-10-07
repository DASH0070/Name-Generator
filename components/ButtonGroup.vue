<script setup lang="ts">

import { Gender, Popularity, Length, names } from '../data';

const props = defineProps<{
    selectedNames?: string[],
    buttonList: { gender: Gender[], popularity: Popularity[], length: Length[] },
    option: { gender: Gender, popularity: Popularity, length: Length }
}>()

// apply class based on current option
const checkClass = (elem: string[], key: string, btn: string, index: number) => {
    let str = '';
    if (index === 0)
        str += ' rounded-l-full ';
    if (index === elem.length - 1)
        str += ' rounded-r-full ';
    if (btn === props.option[key])
        str += ' text-white bg-red-400 ';
    else
        str += ' text-indigo-400 '
    return str;
}

// Button generate Names based on current options
const generateNames = (e: MouseEvent) => {
    props.selectedNames.length = 0;
    for (let i = 0; i < names.length; i++) {
        if (names[i].gender === props.option.gender &&
            (props.option.length === 'All' || names[i].length === props.option.length) &&
            names[i].popularity === props.option.popularity)
            props.selectedNames.push(names[i].name);
    }
    return e;
}

// Change value of option if btn clicked
const btnClick = (e: MouseEvent, key: string) => {
    const target = e.target as HTMLElement;
    props.option[key] = target.innerText;
    return e;
}

</script>

<template>

    <div class="text-center bg-red-100 rounded-[3rem] w-[60rem] mx-auto py-20 ">
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

</template>