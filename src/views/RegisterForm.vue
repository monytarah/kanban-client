<template>
    <body>
        <div class="container">
            <div class="row">
            <div class="col-lg-10 col-xl-9 mx-auto">
                <div class="card card-signin flex-row my-5">
                <div class="card-img-left d-none d-md-flex">
                    <!-- Background image for card set in CSS! -->
                </div>
                <div class="card-body">
                    <h5 class="card-title text-center">Register</h5>
                    <form class="form-signin" @submit.prevent="register">
                    <div class="form-floating mb-3">
                      <input type="email" class="form-control" v-model="email" placeholder="name@example.com">
                      <label for="register-email">Email address</label>
                    </div>
                    <div class="form-floating mb-3">
                      <input type="password" class="form-control" v-model="password" placeholder="Password">
                      <label for="register-password">Password</label>
                    </div>                    
                    <!-- <input class="btn btn-lg btn-google btn-block text-uppercase" type="submit" value="Login"> -->
                    <input class="btn btn-lg btn-primary btn-block text-uppercase" type="submit" value="Register">
                    <hr class="my-4">
                    <h6>Already have account? <a href="#" @click.prevent="changeRegister(false)">Login</a> here!</h6>
                    </form>
                </div>
                </div>
            </div>
            </div>
        </div>
    </body>
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
        url: 'https://kanban-monyta.herokuapp.com/register',
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

<style scoped>
.card-signin {
  border: 0;
  border-radius: 1rem;
  box-shadow: 0 0.5rem 1rem 0 rgba(0, 0, 0, 0.1);
  overflow: hidden;
}

.card-signin .card-title {
  margin-bottom: 2rem;
  font-weight: 300;
  font-size: 1.5rem;
}

.card-signin .card-img-left {
  width: 45%;
  /* Link to your background image using in the property below! */
  background: scroll center url('https://images.unsplash.com/photo-1510845850921-b8f6e35f3c54?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=80');
  background-size: cover;
}

.card-signin .card-body {
  padding: 2rem;
}

.form-signin {
  width: 100%;
}

.form-signin .btn {
  font-size: 80%;
  border-radius: 5rem;
  letter-spacing: .1rem;
  font-weight: bold;
  padding: 1rem;
  transition: all 0.2s;
}
</style>