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
                    <h5 class="card-title text-center">Login</h5>
                    <form class="form-signin" @submit.prevent="login">
                    <div class="form-floating mb-3">
                        <input type="email" class="form-control" v-model="email" placeholder="name@example.com">
                        <label for="login-email">Email address</label>
                    </div>
                    <div class="form-floating mb-3">
                        <input type="password" class="form-control" v-model="password" placeholder="Password">
                        <label for="login-password">Password</label>
                    </div>
                    
                    <!-- <input class="btn btn-lg btn-google btn-block text-uppercase" type="submit" value="Login"> -->
                    <input class="btn btn-primary text-uppercase" type="submit" value="Sign In">                    <hr class="my-4">
                    <GoogleLogin class="mb-3" :params="params" :renderParams="renderParams" :onSuccess="onSuccess"></GoogleLogin>
                    <h6>Don't have account? <a href="#" @click.prevent="changeRegister(true)">Register</a> here!</h6>
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
import GoogleLogin from 'vue-google-login'

export default {
    name: 'LoginForm',
    props: ['changeRegister', 'changeIsLogin'],
    data () {
        return {
            email: '',
            password: '',
            params: {
                client_id: '237644686783-2sdch09tdcnff86cll295q5i7msiq97v.apps.googleusercontent.com'
            },
            renderParams: {
                width: 200, 
                height: 40, 
                longtitle: true
            }
        }
    },
    methods: {
        login(){
            axios({
                method: 'POST',
                url: 'https://kanban-monyta.herokuapp.com/login',
                data: {
                    email: this.email, 
                    password: this.password
                }
            })
                .then(({ data }) =>{
                    // console.log(response)
                    localStorage.setItem('access_token', data.access_token)
                    this.changeIsLogin(true)
                })
                .catch(err => {
                    console.log(err.response)
                })
        },
        onSuccess(googleUser) {
            // console.log(googleUser)
            // console.log('masuk google')
            let id_token = googleUser.getAuthResponse().id_token;
            // console.log(id_token)
            axios({
                method: 'POST',
                url: 'https://kanban-monyta.herokuapp.com/loginGoogle',
                data: { id_token }
            })
                .then(response => {
                    console.log(response)
                    localStorage.setItem('access_token', response.data.access_token)
                    this.changeIsLogin(true)
                })
                .catch(err => {
                    console.log(err)
                })
        }
    },
    components: {
        GoogleLogin
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
  background: scroll center url('https://images.unsplash.com/photo-1512486130939-2c4f79935e4f?ixid=MXwxMjA3fDB8MHxzZWFyY2h8NHx8d29ya3NwYWNlfGVufDB8MnwwfA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=400&q=60');
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