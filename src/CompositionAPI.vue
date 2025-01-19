<script>
import { ref } from "vue";

export default {
  setup() {
    const name = "Patrick Mankaryous";
    const status = ref("active");
    const tasks = ["Task One", "Task Two", "Task Three"];

    // If using reactive variable 'ref()' we don't use this keyword!
    const toggleStatus = () => {
      if (status.value === "active") {
        status.value = "pending";
      } else if (status.value === "pending") {
        status.value = "inactive";
      } else {
        status.value = "active";
      }
    };

    return {
      name,
      status,
      tasks,
      toggleStatus,
    };
  },
};
</script>

<template>
  <header>
    <h1>Vue Jobs</h1>
    <p>{{ name }}</p>
    <p v-if="status === 'active'">User is active</p>
    <p v-else-if="status === 'pending'">User is pending</p>
    <p v-else>User is inactive</p>

    <h3>Tasks:</h3>

    <ul>
      <li v-for="task in tasks" :key="task">
        {{ task }}
      </li>
    </ul>
    <br />

    <!-- <button v-on:click="toggleStatus">Change Status</button> -->

    <!-- Short syntax -->
    <button @click="toggleStatus">Change Status</button>
  </header>
</template>

<style scoped>
h1 {
  color: red;
}
</style>
