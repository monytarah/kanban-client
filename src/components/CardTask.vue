<template>
    <div class="card mb-3">
        <div class="card-body border border-warning">
            <h5 class="card-title">{{ task.title }}</h5>
            <p class="card-text">Created by: {{ task.User.email }}</p>
            <button class="btn btn-success" @click.prevent="findTask(task.id)">Update</button>
            <button class="btn btn-danger"  @click.prevent="deleteTask(task.id)">Delete</button>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    props: ['task', 'fetchTasks', 'updateTask'],
    methods: {
        deleteTask(id) {
            // console.log(id)
            axios({
                method: 'DELETE', 
                url: `http://localhost:3000/tasks/${id}`,
                headers: {
                    access_token: localStorage.access_token
                }
            })
                .then(response => {
                    // console.log(response)
                    this.fetchTasks()
                })
                .catch(err => {
                    console.log(err.response)
                })
        },
        findTask(id) {
            axios({
                method: 'GET', 
                url: `http://localhost:3000/tasks/${id}`,
                headers: {
                    access_token: localStorage.access_token
                }
            })
                .then(response =>{
                    // console.log(response)
                    this.updateTask(response.data)
                    
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