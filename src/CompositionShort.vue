<!-- Short version of the compositionAPI use this! -->

<script setup>
// ref = sort of as useState
// ref is very important if things not reacting check the variable is a ref!
import { onMounted, ref } from "vue";

const name = "Patrick Mankaryous";
const status = ref("active");
const tasks = ref(["Task One", "Task Two", "Task Three"]);
const newTask = ref("");

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

const addTask = () => {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value);
    newTask.value = "";
  }
};

//Normally we do this, but we don't have id's so if a task is the same everything is deleted!
// const deleteTask = (task) => {
//   tasks.value = tasks.value.filter((item) => item !== task);
// };

const deleteTask = (i) => {
  tasks.value.splice(i, 1); // Remove task at the specified index
};

onMounted(async () => {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/todos");
    const todos = await response.json();
    tasks.value = todos.map(({ title }) => title);
  } catch (error) {
    console.error("Error fetching tasks:", error);
  }
});
</script>

<template>
  <header>
    <h1>Vue Jobs</h1>
    <p>{{ name }}</p>
    <p v-if="status === 'active'">User is active</p>
    <p v-else-if="status === 'pending'">User is pending</p>
    <p v-else>User is inactive</p>

    <form @submit.prevent="addTask">
      <label for="newTask">Add Task</label>
      <input type="text" id="newTask" name="newTask" v-model="newTask" />
      <button type="submit">Submit</button>
    </form>

    <h3>Tasks:</h3>

    <ul>
      <li v-for="(task, i) in tasks" :key="task">
        <span>{{ task }}</span>
        <button @click="deleteTask(i)">x</button>
      </li>
    </ul>
    <br />
    <h4>Todos Count:</h4>
    <p>{{ tasks.length }}</p>
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
