<script setup lang="ts">

const option = ref({
    gender: 'Unisex',
    popularity: 'Trendy',
    lenght: 'Short'
})
</script>

<template>

    <div class="text-center p-20">
        <h1 class="text-red-400 text-8xl my-10">Name Generator</h1>
        <div class="bg-red-100 rounded-[3rem] w-[60rem] mx-auto py-20 ">
            <div class="option-container my-8">
                <button :class="option.gender === 'Boy' && 'bg-red-400 active'" class="btn rounded-l-full">Boy</button>
                <button :class="option.gender === 'Unisex' && 'bg-red-400 active'" class="btn">Unisex</button>
                <button :class="option.gender === 'Girl' && 'bg-red-400 active'"
                    class='btn rounded-r-full'>Girl</button>
            </div>
            <div class="option-container my-8">
                <button :class="option.popularity === 'Trendy' && 'bg-red-400 active'"
                    class='btn rounded-l-full'>Trendy</button>
                <button :class="option.popularity === 'Unique' && 'bg-red-400 active'"
                    class='btn rounded-r-full'>Unique</button>
                <div class="option-container my-8">
                    <button :class="option.lenght === 'Long' && 'bg-red-400 active'"
                        class='btn rounded-l-full'>Long</button>
                    <button :class="option.lenght === 'All' && 'bg-red-400 active'" class='btn'>All</button>
                    <button :class="option.lenght === 'Short' && 'bg-red-400 active'"
                        class='btn rounded-r-full'>Short</button>
                </div>
            </div>
        </div>
    </div>

</template>

<style lang="postcss" scoper>
.btn {
    @apply text-2xl w-32 h-14 border-2 border-red-400 text-indigo-400
}

.active {
    @apply text-white
}
</style>
