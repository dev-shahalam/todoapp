<script setup>


</script>

<template>
    <div class="container mx-auto ">

        <div class=" h-svh text-center content-center justify-items-center">

            <!-- Create Task -->
            <div class="w-full">
                <h1 class="text-4xl text-slate-500">Task Management App</h1>
                <button class=" px-5 py-1 my-5 rounded text-white text-lg bg-purple-500 hover:bg-slate-500 transition">Show Add Task Form</button>
                <br>
                <!-- <button>Hide Add Task Form</button> -->

                <input class="w-6/12 border border-slate-300 px-5 py-2 outline-purple-500" type="text"
                    placeholder="Enter Task Name">
                <br>
                <button class="bg-purple-500 hover:bg-slate-500 transition px-2 py-2 my-5 rounded text-white text-sm"> Add Task </button>
            </div>



            <!-- Show Task -->
            <div class="border flex items-center justify-between border-slate-300 w-6/12 text-start px-3 mb-3">
                <div>
                    <p>Task One</p>
                </div>

                <div>
                    <button class="bg-purple-500 hover:bg-slate-500 transition px-2 py-2 my-5 rounded text-white text-sm"> Complete </button>
                    <button class="bg-purple-500 hover:bg-slate-500 transition px-2 py-2 my-5 ml-2 rounded text-white text-sm"> Delete </button>
                </div>

            </div>


        </div>








    </div>
</template>

<style scoped></style>
