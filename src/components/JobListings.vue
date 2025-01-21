<script setup>
import { RouterLink } from "vue-router";
import JobListing from "./JobListing.vue";
import { reactive, defineProps, onMounted } from "vue";
import PulseLoader from "vue-spinner/src/PulseLoader.vue";
import axios from "axios";

defineProps({
  limit: Number,
  showButton: {
    type: Boolean,
    default: false,
  },
});

// ref() is comparable with const [name, setName] = useState([]);
// reactive({}) is comparable with [form, setForm] = useState({firstName:'', lastName:''});

// const jobs = ref([])

const state = reactive({
  jobs: [],
  isLoading: true,
});

// onMouted is comparable with useEffect
onMounted(async () => {
  try {
    const response = await axios.get("/api/jobs");
    state.jobs = response.data;
  } catch (error) {
    console.error("Error fetching jobs", error);
  } finally {
    state.isLoading = false;
  }
});

// Re-assign: state = ...
// No re-assign: state.isLoading = ...

// We use jobs.value because it is a ref!
// console.log(jobs.value);
</script>

<template>
  <section class="bg-blue-50 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
        Browse Jobs
      </h2>

      <!-- Show loading spinner when isLoading -->
      <div v-if="state.isLoading" class="text-center text-gray-500 py-6">
        <PulseLoader />
      </div>

      <!-- Show JobListing when !isLoading -->
      <div v-else class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <!-- bind job to the JobListing component!! -->
        <JobListing
          v-for="job in state.jobs.slice(0, limit || state.jobs.length)"
          :key="job.id"
          :job="job"
        />
      </div>
    </div>
  </section>
  <section v-if="showButton" class="m-auto max-w-lg my-10 px-6">
    <RouterLink
      to="/jobs"
      class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
      >View All Jobs</RouterLink
    >
  </section>
</template>
