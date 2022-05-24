<template>
  <Header :total="10"/>

  <section v-if="error" class="h-80 w-full flex justify-center items-center">
    <Error/>
  </section>

<!-- loading -->
  <section class="v-else">
    <div v-if="loading">
    <Loader/>
  </div>

<!-- main body section -->

<div v-else class="container m-auto pt-4 flex justify-between w-full gap-5">
<section>
   <task-header :taskTitle="taskTitle[0]" :count="backlog.length"> 
  <i class="fa-solid fa-circle-dashed text-red-500"></i> 
  </task-header>
<draggable group="tasks" v-model="backlog">
<task-card v-for="(task) in backlog" :key="task.id" :task="task" class="cursor-move">
  </task-card>
  </draggable>
</section>
  

   <section>
  <task-header :taskTitle="taskTitle[1]" :count="todos.length"> 
  <i class="fa-solid fa-circle-notch text-white"></i>
  </task-header>
<draggable group="tasks" v-model="todos">
<task-card v-for="(task) in todos" :key="task.id" :task="task" class="cursor-move">
  </task-card>
  </draggable>
</section>

<section>
  <task-header :taskTitle="taskTitle[2]" :count="inprogress.length"> 
    <i class="fa-solid fa-circle-half-stroke text-yellow-300"></i>
  </task-header>
<draggable group="tasks" v-model="inprogress">
<task-card v-for="(task) in inprogress" :key="task.id" :task="task" class="cursor-move">
  </task-card>
  </draggable>
</section>

   <section>
  <task-header :taskTitle="taskTitle[3]" :count="done.length"> 
    <i class="fa-solid fa-circle-check text-green-500"></i>
  </task-header>
<draggable group="tasks" v-model="done">
<task-card v-for="(task) in done" :key="task.id" :task="task" class="cursor-move">
  </task-card>
  </draggable>
</section>
</div>
  </section> 
  
</template>

<script>
import axios from 'axios';
 import { VueDraggableNext } from 'vue-draggable-next'
import Header from './components/Header.vue'
import Error from './components/Error.vue';
import TaskCard from './components/TaskCard.vue';
import TaskHeader from './components/TaskHeader.vue';
import Loader from './components/Loader.vue';
export default {
  name: 'App',
  components: {
    Header,
    Error,
    draggable: VueDraggableNext,
    TaskCard,
    TaskHeader,
    Loader
},
data(){
return {
      tasks:[],
      loading: true,
      error: false,
      backlog:[],
      todos:[],
      inprogress:[],
      done:[],
      taskTitle:['Backlog','Todo','In Progress','Done']
    }
},
mounted () {
    axios
      .get('http://localhost:4000/items')
      .then(response => {
      
        this.tasks=response?.data;
        
        // this.backlog=response.data.filter(function(val){
        //     return val?.status==="backlog";
        // })
        // this.done=response.data.filter(function(val){
        //     return val?.status==="done";
        // })
        // this.inprogress=response.data.filter(function(val){
        //     return val?.status==="in-progress";
        // })
        // this.todos=response.data.filter(function(val){
        //     return val?.status==="todo";
        // })

        this.backlog=response.data[0].items;

        this.todos=response.data[1].items
        this.inprogress=response.data[2].items
        this.done=response.data[3].items;
        
      })
      .catch(error => {
        console.log(error?.message)
        this.error = true
      })
      .finally(() => this.loading = false)
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body{
  background: #1c1d1f;
}
</style>
