<template>
  <div class="p-3">
    <div class="card p-2 shadow-sm mb-3">
      <h5>{{ value.title }}</h5>
      <p class="text-muted">{{ value.description }}</p>
      <p>{{ value.User.email }}</p>
      <b-button v-b-modal.modal-2 @click="getId">Edit</b-button>
      <button @click="getId"><i class="far fa-hand-point-left"></i></button>
      <button @click="getIdForward"><i class="far fa-hand-point-right"></i></button>
      <button @fetchtasks='fetchTasks' @click.prevent="deleteTask"><i class="fas fa-trash"></i></button>
    </div>
  </div>
</template>

<script>
import axios from '../config/axios'
export default {
  name: "CardTask",
  props: ["value"],
  methods: {
    getId() {
      this.$emit("getTaskId", this.value);
    },
    getIdForward() {
      this.$emit('taskForward', this.value)
    },
    deleteTask() {
      axios({
        method: 'DELETE',
        url: `/tasks/${this.value.id}`,
        headers: {
          access_token: localStorage.access_token
        }
      })
      .then(data => {
        this.fetchTasks()
      })
    },
    fetchTasks() {
      this.$emit('fetchTasks')
    }
  },
};
</script>

<style></style>
