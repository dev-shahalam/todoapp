<script setup>
import {reactive, ref} from "vue";

const isActive=ref(false);
const msg=ref('Show Add Task Form')


function toggleForm(){
   isActive.value=!isActive.value;
   msg.value=isActive.value?'Hide Add Task Form':'Show Add Task Form';
}

const task=ref('');
const taskList=ref([]);

function addTask(){
task.value.trim().split(/\s+/);
if (task.value==='' || task.value.length<3) return alert('Please Enter Task Name & Min 3 Characters')
taskList.value.push(task.value);
task.value='';
}


function deleteTask(index){
  taskList.value.splice(index,1);
}

const complatedStyle=ref({
  backgroundColor:'green'
})

const completedTask=ref(false)


function completeTask(){
 completedTask.value=!completedTask.value;
}

</script>

<template>
    <div class="container mx-auto ">

        <div class=" h-svh text-center content-center justify-items-center">

            <!-- Create Task -->
            <div class="w-full">
                <h1 class="text-4xl text-slate-500">Task Management App</h1>
                <button  class=" px-5 py-1 my-5 rounded text-white text-lg bg-purple-500 hover:bg-slate-500 transition" @click="toggleForm()"
                >{{msg}}</button>
                <br>
              <div v-show="isActive" >
                <input v-model="task" class="w-6/12 border border-slate-300 px-5 py-2 outline-purple-500" type="text"
                    placeholder="Enter Task Name">
                <br>
                <button @click="addTask()" class="bg-purple-500 hover:bg-slate-500 transition px-2 py-2 my-5 rounded text-white text-sm"> Add Task </button>
              </div>
              </div>



            <!-- Show Task -->
          <h4 v-show="taskList.length===0" >No Task Available Here</h4>
            <div :style="completedTask===true?'completedStyle':'background-color:red'" v-for="(task,index) in taskList" :key="index" class="border flex items-center justify-between border-slate-300 w-6/12 text-start px-3 mb-3">
                <div>
                  <p>{{completedTask}}</p>
                    <p>{{task}}</p>
                </div>

                <div>
                    <button @click="completeTask()" class="bg-purple-500 hover:bg-slate-500 transition px-2 py-2 my-5 rounded text-white text-sm"> Complete </button>
                    <button @click="deleteTask(index)" class="bg-purple-500 hover:bg-slate-500 transition px-2 py-2 my-5 ml-2 rounded text-white text-sm"> Delete </button>
                </div>

            </div>


        </div>








    </div>
</template>

<style scoped></style>
