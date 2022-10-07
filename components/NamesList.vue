<script setup lang="ts">

const props = defineProps<{ selectedNames: string[] }>();
const emit = defineEmits(['click'])

</script>

<template>

    <ul class="flex justify-center gap-8 flex-wrap my-8">
        <li class="text-red-400 text-xl" v-for="(names, index) in props.selectedNames" :key="names">{{names}}
            <!-- <button @click="(e: MouseEvent) => removeName(e, names)" class="text-black">X</button> -->
            <button @click="(e: MouseEvent) => emit('click', index)" class="text-black">X</button>
        </li>
    </ul>

</template>