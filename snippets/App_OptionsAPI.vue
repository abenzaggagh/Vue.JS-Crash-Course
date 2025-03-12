<script>
  export default {
    data() {
      return {
        name: "Amine BEN ZAGGAGH",
        status: "pending",
        tasks: ['Task 1', 'Task 2', 'Task 3', 'Task 4'],
        link: 'https://google.com',
      }
    }, methods: {
      toggleStatus() {
        if (this.status === "active") {
          this.status = "pending";
        } else if (this.status === "pending") {
          this.status = "inactive";
        } else {
          this.status = "active";
        }
      }
    }
  }
</script>

<template>
  <h1>Vue.JS Crash Course</h1>
  <h2>{{ name }}</h2>
  <p v-if="status === 'active'">User is active.</p>
  <p v-else-if="status === 'pending'">User is pending.</p>
  <p v-else>User is inactive.</p>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>

  <a v-bind:href="link">Click for Google</a>

  <button @click="toggleStatus">Toggle Status</button>

</template>

<style scoped>

</style>