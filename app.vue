<script setup lang="ts">
const buttonList = {
    gender: ['Boy', 'Unisex', 'Girl'],
    popularity: ['Trendy', 'Unique'],
    length: ['Long', 'All', 'Short']
};
const option = ref({
    gender: 'Unisex',
    popularity: 'Trendy',
    length: 'Short'
});

const checkClass = (elem: string[], key: string, btn: string, index: number) => {
    let str = '';
    if (index === 0)
        str += ' rounded-l-full '
    if (index === elem.length - 1)
        str += ' rounded-r-full '
    if (btn === option.value[key])
        str += ' active '
    return str;
}

const btnClick = (e: MouseEvent, key: string) => {
    const target = e.target as HTMLElement;
    option.value[key] = target.innerText;
    return e;
}

</script>

<template>

    <div class="text-center p-20">
        <h1 class="text-red-400 text-8xl my-10">Name Generator</h1>
        <div class="bg-red-100 rounded-[3rem] w-[60rem] mx-auto py-20 ">
            <div v-for="(elem, key) in buttonList" class="option-container my-8">
                <button v-for="(btn, index) in elem" class="btn" :class="checkClass(elem, key, btn, index)"
                    @click="(e: MouseEvent) => btnClick(e, key)">
                    {{btn}}
                </button>
            </div>
        </div>
    </div>

</template>

<style lang="postcss" scope>
.btn {
    @apply text-2xl w-32 h-14 border-2 border-red-400 text-indigo-400
}

.active {
    @apply text-white bg-red-400
}
</style>
