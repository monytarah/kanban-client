<template>
  <div class="col-6 mx-auto my-4">
    <h5>Add Task</h5>
    <form @submit.prevent="addTask">
      <div class="form-group mb-3">
        <label class="mb-2" for="add-title">Title</label>
        <input type="text" class="form-control" v-model="title" placeholder="Swim">
      </div>
      <div class="form-group mb-3">
        <label class="mb-2">Category</label>
        <select class="form-select" v-model="category">
          <option value="Backlog">Backlog</option>
          <option value="To Do">To Do</option>
          <option value="In Progress">In Progress</option>
          <option value="Done">Done</option>
        </select>
      </div>   
      <button type="submit" class="btn btn-success">Submit</button>
      <button type="button" class="btn btn-secondary" @click.prevent="changeAddTask(false)">Cancel</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'AddForm',
    props: ['changeAddTask'],
    data(){
      return {
        title: '',
        category: ''
      }
    },
    methods: {
      addTask() {
        axios({
          method: 'POST', 
          url: 'http://localhost:3000/tasks',
          data: {
            title: this.title, 
            category: this.category
          },
          headers: {
            access_token: localStorage.access_token
          }
        })
          .then(() => {
            this.changeAddTask(false)
          })
          .catch(err => {
            console.log(err.response)
          })
      }
    }
}
</script>

<style>

</style>