<template>
  <div class="bg-stone-900 shadow rounded px-3 pt-3 pb-5 border border-gray-900 w-80 min-w-80 mb-3">
    <div class="flex justify-between">
        <div>
      <p class="text-gray-600 font-semibold font-sans tracking-wide text-sm">{{task?.id}}</p>
      <span class="text-sm text-white">{{task?.name}}</span>
        </div>

      <img
        class="w-6 h-6 rounded-full ml-3"
        src="https://pickaface.net/gallery/avatar/unr_sample_161118_2054_ynlrg.png"
        alt="Avatar"
      >
    </div>
    <div class="flex mt-4 justify-between items-center">
      <i class="fa-solid fa-signal text-gray-600"></i>
    </div>
  </div>
</template>


<script>
export default{
    name:'TaskCard',
    props:{
    task: {
      type: Object,
      default: () => ({})
    }
    }
}

</script>