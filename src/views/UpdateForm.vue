<template>
  <div class="col-6 mx-auto my-4">
    <h5>Update Task</h5>
    <form @submit.prevent="updateTask">
      <div class="form-group mb-3">
        <label class="mb-2" for="update-title">Title</label>
        <input type="text" v-model="title" class="form-control" id="update-title" placeholder="Swim">
      </div>
      <div class="form-group mb-3">
        <label class="mb-2">Category</label>
        <select v-model="category" class="form-select" aria-label="Default select example">
          <option value="Backlog">Backlog</option>
          <option value="To Do">To Do</option>
          <option value="In Progress">In Progress</option>
          <option value="Done">Done</option>
        </select>
      </div>   
      <button type="submit" class="btn btn-success">Update</button>
      <button type="button" class="btn btn-secondary" @click.prevent="changeUpdateTask(false)">Cancel</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'UpdateForm',
    props: ['dataUpdate', 'changeUpdateTask'],
    data() {
      return {
        title: this.dataUpdate.title,
        category: this.dataUpdate.category,
        id: this.dataUpdate.id
      }
    },
    methods: {
      updateTask(){
        axios({
          method: 'PUT',
          url: `http://localhost:3000/tasks/${this.id}`, 
          headers: {
            access_token: localStorage.access_token
          },
          data: {
            title: this.title, 
            category: this.category
          }
        })
          .then(response => {
            this.changeUpdateTask(false)
          })
          .catch(err => {
            console.log(err)
          })
      }
    }
}
</script>

<style>

</style>