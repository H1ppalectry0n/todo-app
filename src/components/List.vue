<template>
  <div>
    <div v-if="tasksList.length">
      <div
        class="row"
        v-for="task of tasksList"
        :key="task.id"
        v-bind:class="{ complete: task.complited }"
      >
        <button class="btn-danger" v-on:click="$emit('deleteTask', task.id)">
          X
        </button>
        <p v-on:click="$emit('setStatus', task.id)">{{ task.title }}</p>
        <button class="btn-warning" v-on:click="$emit('editTask', task.id)">
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
