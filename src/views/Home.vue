<template>
  <div class="container row flex-row mx-auto mb-5">
    <Category :updateTask="updateTask" :fetchTasks="fetchTasks" :tasks="tasks" v-for="category in categories" :key="category.id" :category="category"></Category>
  </div>
</template>

<script>
import axios from 'axios'
import Category from "../components/Category.vue";
export default {
  name: "Home",
  props: ['updateTask'],
  data() {
    return {
      categories: [
        { id: 1, name: 'Backlog'},
        { id: 2, name: 'To Do'},
        { id: 3, name: 'In Progress'},
        { id: 4, name: 'Done'},
      ],
      tasks: []
    }
  },
  components: { 
    Category 
  },
  methods: {
    fetchTasks() {
      axios({
        method: 'GET', 
        url: 'http://localhost:3000/tasks',
        headers: {
          access_token: localStorage.access_token
        }
      })
        .then(({data}) => {
          this.tasks = data
          // console.log(this.tasks)
        })
        .catch(err => {
          console.log(err)
        })
    }
  },
  created() {
    this.fetchTasks()
  }
};
</script>

<style>
</style>