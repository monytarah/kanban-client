<template>
    <div class="card mb-3">
        <div class="card-body border">
            <h6 class="card-title">{{ task.title }}</h6>
            <!-- <p class="card-text h6">Created by: {{ task.User.email }}</p> -->
            <p class="mb-0"><small>created by: {{ task.User.email }}</small></p>

            <div class="float-end">
                <button class="btn pb-0" @click.prevent="findTask(task.id)"><i class="fas fa-edit"></i></button>
                <button class="btn pb-0" @click.prevent="deleteTask(task.id)"><i class="fas fa-trash-alt"></i></button>
            </div>
            <!-- <button class="btn btn-success" @click.prevent="findTask(task.id)">Update</button>
            <button class="btn btn-danger"  @click.prevent="deleteTask(task.id)">Delete</button> -->
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
                url: `https://kanban-monyta.herokuapp.com/tasks/${id}`,
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
                url: `https://kanban-monyta.herokuapp.com/tasks/${id}`,
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