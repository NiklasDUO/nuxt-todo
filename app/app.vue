<template>
  <div class="grid place-items-center bg-slate-800">
    <h1 class="text-4xl text-white font-mono py-10">My TODOs</h1>
    <div class="flex justify-center w-1/2 items-center mb-4">
      <input
        class="p-1 text-center mr-10 h-10 bg-slate-500 text-white font-mono rounded-md"
        type="text"
        placeholder="Add new TODO"
        v-model="newTask"
        @keypress.enter="addTask"
      />
      <button
        class="rounded-md bg-green-500 text-white font-mono h-10 w-32 text-2xl"
        @click="addTask"
      >
        Add
      </button>
    </div>
  </div>
  <div class="grid place-items-center bg-slate-950 h-screen">
    <div class="w-1/2 flex justify-center" style="left:50%">
      <ul class="w-1/2 p-4 justify-center flex flex-col">
        <li v-for="(task, index) in tasks" :key="index" class="text-white font-mono m-4 flex justify-center flex-col">
          <span :class="{ 'line-through': task.completed }" class="text-center">{{ task.name }}</span>
          <div class="flex mt-2 justify-center">
            <button
              class="bg-red-500 text-white font-mono h-8 w-8 rounded-md"
              @click="deleteTask(index)"
            >
              X
            </button>
            <button
              :class="{ 'bg-green-500': task.completed, 'bg-gray-500': !task.completed }"
              class="text-white font-mono h-8 w-8 rounded-md ml-2"
              @click="toggleTaskCompletion(index)"
            >
              ✓
            </button>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>


<script>
export default {
  name: 'App',
  data() {
    return {
      tasks: [],
      newTask: '',
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({
          name: this.newTask,
          completed: false
        });
        this.newTask = '';
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    toggleTaskCompletion(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
    },
  },
};
</script>
