<template>
  <nav>
    <div class="navbar navbar-light bg-light shadow">
      <div class="container d-flex justify-content-between">
        <a href="#" class="navbar-brand d-flex align-items-center">
          <strong>Kanban App</strong>
        </a>
        <div class="ml-auto">
          <button class="btn btn-success" v-if="isLogin && !showUpdate" @click.prevent="changeAddTask(true)">Add Task</button>
          <button class="btn btn-danger" v-if="isLogin" @click.prevent="logout">Logout</button>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import axios from 'axios'
export default {
    name: 'Navbar',
    props: ['isLogin', 'changeAddTask', 'changeIsLogin', 'showUpdate'],
    methods: {
      logout() {
        localStorage.clear()
        let auth2 = gapi.auth2.getAuthInstance();
        // console.log(auth2)
        auth2.signOut().then(function () {
          console.log('User signed out.');
        });
        this.changeAddTask(false)
        this.changeIsLogin(false)
      }
    }
}
</script>

<style>

</style>