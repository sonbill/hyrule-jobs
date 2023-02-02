<template>
  <div class="app">
    <div class="flex justify-center items-center space-x-5">
      <img src="@/assets/heart.svg" alt="heart" class="w-[60px]" />
      <h1 class="title text-3xl font-bold">Hyrule Jobs</h1>
    </div>
    <!-- HEADER BUTTONS -->
    <div class="text-center mt-10">
      <button @click="handleClick('title')" class="p-3 border rounded-md mx-5">
        Order by Title
      </button>
      <button @click="handleClick('salary')" class="p-3 border rounded-md mx-5">
        Order by Salary
      </button>
      <button
        @click="handleClick('location')"
        class="p-3 border rounded-md mx-5"
      >
        Order by Location
      </button>
    </div>
    <JobsList :jobs="jobs" :order="order" />
  </div>
</template>

<script lang="ts">
import JobsList from "./components/JobsList.vue";
import type Job from "./types/Job";
import type OrderTerm from "./types/OrderTerm";
import { RouterLink, RouterView } from "vue-router";
import { defineComponent, reactive, ref, toRefs } from "vue";

export default defineComponent({
  name: "App",
  components: { JobsList },
  setup() {
    const jobs = ref<Job[]>([
      { title: "Farm Worker", location: "Ranch", salary: 10000, id: "1" },
      { title: "Quaryman", location: "Death Mountain", salary: 30000, id: "2" },
      {
        title: "Flute Player",
        location: "The Lost Woods",
        salary: 1000,
        id: "3",
      },
      { title: "Fisher man", location: "Lake Hylia", salary: 20000, id: "4" },
      {
        title: "Prison Guard",
        location: "Gerudo Valley",
        salary: 25000,
        id: "5",
      },
    ]);

    const order = ref<OrderTerm>("title");
    const handleClick = (term: OrderTerm) => {
      order.value = term;
      console.log(term);
    };

    return { jobs, order, handleClick };
  },
});
</script>

<style>
</style>