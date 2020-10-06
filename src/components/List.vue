<template>
  <div>
    <div v-if="tasksList.length">
      <div
        class="row"
        v-for="(task, index) of tasksList"
        :key="task.id"
        v-bind:class="{ complete: task.isComplete }"
      >
        <button class="btn-danger" v-on:click="$emit('deleteTask', task.id)">
          X
        </button>
        <p v-on:click="$emit('setStatus', index)">{{ task.title }}</p>
        <button class="btn-warning" v-on:click="$emit('editTask', index)">
          Редактировать
        </button>
      </div>
    </div>
    <div v-else>
      <p>Добавте задачи</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["tasksList"],
};
</script>
