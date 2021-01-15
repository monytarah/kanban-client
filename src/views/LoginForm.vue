<template>
    <div class="col-3 mx-auto my-4" id="login-page">
        <h2>Login</h2>
        <form @submit.prevent="login">
        <div class="form-floating mb-3">
            <input type="email" class="form-control" v-model="email" placeholder="name@example.com">
            <label for="login-email">Email address</label>
        </div>
        <div class="form-floating mb-3">
            <input type="password" class="form-control" v-model="password" placeholder="Password">
            <label for="login-password">Password</label>
        </div>
        <input class="btn btn-primary" type="submit" value="Login">
        </form><br>
        <GoogleLogin class="mb-3" :params="params" :renderParams="renderParams" :onSuccess="onSuccess"></GoogleLogin>
        <h6>Don't have account? <a href="#" @click.prevent="changeRegister(true)">Register</a> here!</h6>
    </div>
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
                client_id: '237644686783-anljj8k7g121ndphcpub6c5u41lqjsn6.apps.googleusercontent.com'
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
                url: 'http://localhost:3000/login',
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
                url: 'http://localhost:3000/loginGoogle',
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

<style>

</style>