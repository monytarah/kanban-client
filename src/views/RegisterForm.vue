<template>
  <div class="col-3 mx-auto my-4" id="register-page">
    <h2>Register</h2>
    <form @submit.prevent="register">
      <div class="form-floating mb-3">
        <input type="email" class="form-control" v-model="email" placeholder="name@example.com">
        <label for="register-email">Email address</label>
      </div>
      <div class="form-floating mb-3">
        <input type="password" class="form-control" v-model="password" placeholder="Password">
        <label for="register-password">Password</label>
      </div>
      <input class="btn btn-primary" type="submit" value="Register">
    </form><br>
    <h6>Already have account? <a href="#" @click.prevent="changeRegister(false)">Login</a> here!</h6>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'RegisterForm',
  data() {
    return {
      email: '',
      password: ''
    }
  },
  props: ['changeRegister'],
  methods: {
    register() {
      axios({
        method: 'POST',
        url: 'http://localhost:3000/register',
        data: {
          email: this.email, 
          password: this.password
        }
      })
        .then(()=>{
          this.changeRegister(false)
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