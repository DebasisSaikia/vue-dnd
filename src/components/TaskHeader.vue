<template>
     <div class="border-b-2 border-slate-700 mb-3 flex items-center gap-3 pb-3">
        <slot></slot>
        <h1 class="text-white text-xl capitalize">
            {{taskTitle}}
            <span class="text-lg ml-2 text-gray-600">{{count}}</span>
        </h1>
  </div>
</template>

<script>
export default{
    name:'TaskHeader',
    props:['taskTitle','count']
}
</script>