<template>
  <div class="status-container">
    <div class="upper-status">
      <span>{{ status }}</span>
      <span class="task-number">{{ length }}</span>
        <span class="icons">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="settings-svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M5 12h.01M12 12h.01M19 12h.01M6 12a1 1 0 11-2 0 1 1 0 012 0zm7 0a1 1 0 11-2 0 1 1 0 012 0zm7 0a1 1 0 11-2 0 1 1 0 012 0z"
            />
          </svg>
          <NuxtLink :to="`/${status}/add`" class="add-task">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="plus-svg"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M12 4v16m8-8H4"
            />
          </svg>
          </NuxtLink>
        </span>
    </div>
    <Container @drop="onDrop">
      <Draggable v-for="task in tasks" :key="task.id">
        <Task :task="task" />
      </Draggable>
    </Container>
    <NuxtLink :to="`/${status}/add`" class="add-task"
      ><span>+ New</span></NuxtLink
    >
  </div>
</template>

<script>
import { Container, Draggable } from "vue-smooth-dnd";
export default {
  props: ["status"],
  components: { Container, Draggable },
  computed: {
    tasks() {
      return this.$store.getters.getTaskByStatus(this.status);
    },
    length() {
      return this.$store.getters.getTaskLengthByStatus(this.status);
    },
  },
  methods: {
    onDrop(dropResult) {
      console.log(dropResult);
    },
  },
};
</script>

<style scoped>
.status-container {
  display: flex;
  flex-direction: column;
  width: 200px;
  padding-left: 20px;
}
.upper-status {
  display: flex;
  align-items: center;
}
.add-task {
  text-decoration: none;
  color: #bcbbba;
  margin-top: 0.5rem;
}
.task-number {
  color: #bcbbba;
  padding-left: 0.8rem;
}
.icons {
  padding-left: 4.4rem;
  color: #bcbbba;
}
.settings-svg {
  height: 15px;
  width: 15px;
}
.plus-svg {
  height: 15px;
  width: 15px;
}
</style>