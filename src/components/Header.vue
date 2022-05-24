<template>
    <header class="h-20 w-full bg-neutral-900 border-0 border-b-2 border-gray-600 flex justify-start items-center">
        <span class="text-white pl-12 text-lg">Board </span> <span class="text-gray-500 ml-2">{{total}}</span>
    </header>
</template>

<script>
export default{
    name:'Header',
    props:['total']
}
</script>