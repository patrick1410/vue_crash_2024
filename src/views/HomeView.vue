<script setup>
import Hero from "@/components/Hero.vue";
import HomeCards from "@/components/HomeCards.vue";
import JobListings from "@/components/JobListings.vue";
</script>

<template>
  <Hero />
  <HomeCards />
  <!-- :limit="3" ! limit="3" because it is a number! -->
  <JobListings :limit="3" :show-button="true" />
</template>
