<template>
  <div class="max-w-[960px] mx-auto">
    <p class="text-xl text-gray-400">Ordered by {{ order }}</p>
    <transition-group name="list" tag="ul" class="p-0">
      <li
        v-for="job in orderedJobs"
        :key="job.id"
        class="bg-white my-[16px] p-[16px] border rounded-lg"
      >
        <h2 class="uppercase my-2 text-xl font-bold">
          {{ job.title }} in {{ job.location }}
        </h2>
        <div class="flex items-center space-x-2">
          <img src="@/assets/rupee.svg" alt="rupee" class="w-[30px]" />
          <p class="font-bold text-green-500">{{ job.salary }} rupees</p>
        </div>
        <div>
          <p class="whitespace-normal text-justify ...">
            Lorem ipsum dolor sit amet consectetur, adipisicing elit. Amet sequi
            fuga quidem debitis doloremque atque unde! Odio inventore minus quod
            neque deleniti eum, maxime itaque! Asperiores, quam voluptatum
            nostrum voluptate quas, consectetur, facilis dicta fugit incidunt
            animi necessitatibus aliquid porro impedit. Accusamus unde enim
            ullam quas fugiat facilis repudiandae necessitatibus.
          </p>
        </div>
      </li>
    </transition-group>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType, computed } from "vue";
import type Job from "@/types/Job";
import type OrderTerm from "@/types/OrderTerm";

export default defineComponent({
  props: {
    jobs: {
      required: true,
      type: Array as PropType<Job[]>,
    },
    order: {
      required: true,
      type: String as PropType<OrderTerm>,
    },
  },
  setup(props) {
    const orderedJobs = computed(() => {
      return [...props.jobs].sort((a: Job, b: Job) => {
        return a[props.order] > b[props.order] ? 1 : -1;
      });
    });

    return { orderedJobs };
  },
});
</script>

<style>
.list-move {
  transition: all 1s;
}
</style>
