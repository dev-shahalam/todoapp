<script setup>

import {reactive, ref, onMounted, onBeforeMount} from "vue";




const isActive = ref(false);
const msg = ref('Show Add Task Form')


function toggleForm() {
    isActive.value = !isActive.value;
    msg.value = isActive.value ? 'Hide Add Task Form' : 'Show Add Task Form';
}

// task store
const newTask = ref('');

let taskList = reactive([]);



// Add task function
function addTask() {
  newTask.value.trim().split(/\s+/);
    if (newTask.value === '' || newTask.value.length < 3) return alert('Please Enter Task Name & Min 3 Characters')
    taskList.push({
        name: newTask.value,
        status: false,
    });
  saveTasks();
  newTask.value = '';

}
// localStorage.clear()

let comStyle =({
  backgroundColor: '#88e788',
  border: '1px solid red'
} )

// Delete Task Function
function deleteTask(index) {
    taskList.splice(index, 1);
    // saveTasks();
}

// localStorage.clear();

function completeTask(index) {

    taskList[index].status = !taskList[index].status;
    saveTasks();


}

let search = ref('');

let getFilteredList=function getFilteredList() {
    return taskList.filter(task => {
        return task.name.toLowerCase().startsWith(search.value.toLowerCase())
    })
}


const saveTasks = () => {
  localStorage.setItem('tasks', JSON.stringify(taskList));
};

const loadTasks = () => {
  let savedData = localStorage.getItem('tasks');
  if (savedData){
    taskList = JSON.parse(savedData);
  }

};


loadTasks();
// localStorage.clear();






</script>

<template>
    <div class="container mx-auto ">
        <div class=" h-svh text-center content-center justify-items-center">
            <!-- Create Task -->
            <div class="w-full">
                <h1 class="text-4xl text-slate-500">Task Management App</h1>
                <button class=" px-5 py-1 my-5 rounded text-white text-lg bg-purple-500 hover:bg-slate-500 transition"
                    @click="toggleForm()">{{ msg }}</button>
                <br>
                <div v-show="isActive">
                    <input v-model="newTask" class="w-6/12 border border-slate-300 px-5 py-2 outline-purple-500"
                        type="text" placeholder="Enter Task Name">
                    <br>
                    <button @click="addTask()"
                        class="bg-purple-500 hover:bg-slate-500 transition px-2 py-2 my-5 rounded text-white text-sm">
                        Add Task </button>
                </div>
            </div>

            <!-- Show Task -->
            <div class=" w-6/12 text-start my-4">
                <input class="px-2 py-2 border border-slate-400 rounded-sm outline-none" v-show="taskList.length !== 0"
                    v-model="search" type="text" placeholder="Search Task">

                <h4 v-show="taskList.length === 0">No tasks available</h4>
            </div>
            <div :style="task.status === true ? comStyle : ''" v-for="(task, index) in getFilteredList()" :key="index"
                class="border rounded-md transition flex items-center justify-between border-slate-300 w-6/12 text-start px-3 mb-3">
                <div>
                    <p>{{ task.name }}</p>
                </div>

                <div>
                    <button @click="completeTask(index)"
                        class="bg-purple-500 hover:bg-slate-500 transition px-2 py-2 my-5 rounded text-white text-sm">
                        {{ task.status === true ? 'Completed' : 'Complete' }} </button>

                    <button @click="deleteTask(index)"
                        class="bg-purple-500 hover:bg-slate-500 transition px-2 py-2 my-5 ml-2 rounded text-white text-sm">
                        Delete </button>
                </div>

            </div>


        </div>








    </div>
</template>

<style scoped></style>
