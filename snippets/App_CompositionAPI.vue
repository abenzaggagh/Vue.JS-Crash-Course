<script setup>
import { onMounted, ref } from "vue";

const name = ref("Amine BEN ZAGGAGH");
const status = ref("active");
const tasks = ref(["Task 1", "Task 2", "Task 3"]);
const newTask = ref("");

const toggleStatus = () => {
  if (status.value === "active") {
    status.value = "pending";
  } else if (status.value === "pending") {
    status.value = "inactive";
  } else {
    status.value = "active";
  }
}

const addTask = () => {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value);
    newTask.value = "";
  }
}

const removeTask = (index) => {
  tasks.value.splice(index, 1);
}

onMounted(async () => {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/todos");
    const data = await response.json();
    tasks.value = data.map(item => {
      return item.title;
    });
  } catch (error) {
    console.log(error);
  }
})
</script>

<template>
  <h1>Vue.JS Crash Course</h1>
  <h2>{{ name }}</h2>
  <p v-if="status === 'active'">User is active.</p>
  <p v-else-if="status === 'pending'">User is pending.</p>
  <p v-else>User is inactive.</p>

  <form @submit.prevent="addTask">
    <label for="new-task">Add Task</label>
    <input type="text" id="new-task" name="new-task" v-model="newTask" />
    <button type="submit">Submit</button>
  </form>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>{{ task }}</span>
      <button @click="removeTask(index)">X</button>
    </li>
  </ul>

  <a v-bind:href="link">Click for Google</a>
  <br />
  <button @click="toggleStatus">Toggle Status</button>

</template>

<style scoped>

</style>