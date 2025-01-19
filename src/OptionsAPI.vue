<script>
export default {
  data() {
    return {
      name: "Patrick Mankaryous",
      status: "pending",
      tasks: ["Task One", "Task Two", "Task Three"],
      google_link: "https://www.google.com",
      dailydev_link: "https://daily.dev",
    };
  },

  methods: {
    toggleStatus() {
      if (this.status === "active") {
        this.status = "pending";
      } else if (this.status === "pending") {
        this.status = "inactive";
      } else {
        this.status = "active";
      }
    },
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

    <a v-bind:href="google_link">Google</a>

    <!-- Short syntax -->
    <a :href="dailydev_link">Daily Dev</a>

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
