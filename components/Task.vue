<template>
  <NuxtLink :to="`/${task.id}`" class="container">
    <span>{{ task.task }}</span>
    <span
      v-on:click.prevent
      @click="
        () => {
          removeTask(task.id);
        }
      "
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="delete"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"
        />
      </svg>
    </span>
  </NuxtLink>
</template>

<script>
import { mapMutations } from "vuex";
export default {
  props: ["task"],
  methods: {
    ...mapMutations(["removeTask"]),
  },
};
</script>

<style scoped>
.container {
  display: flex;
  justify-content: space-between;
  padding: 0.5rem 1rem;
  text-decoration: none;
  color: black;
  border: 1px solid rgb(229,229,229);
  border-radius: 3px;
  margin-top: 0.8rem;
}
.delete {
  height: 15px;
  width: 15px;
}
</style>