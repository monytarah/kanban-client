<template>
  <nav>
    <div class="navbar navbar-dark bg-dark" v-if="isLogin">
      <div class="container d-flex justify-content-between">
        <a href="#" class="navbar-brand d-flex align-items-center">
          Kanban App
        </a>
        <div class="ml-auto">
          <button class="btn btn-dark" v-if="isLogin && !showUpdate" @click.prevent="changeAddTask(true)">Add Task</button>
          <button class="btn btn-dark" v-if="isLogin" @click.prevent="logout">Logout</button>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>

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