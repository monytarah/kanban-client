<template>
    <div>
    <div v-if="isLogin">
        <div class="background-style">
        <Navbar :isLogin="isLogin" :changeIsLogin="changeIsLogin" :changeAddTask="changeAddTask" :showUpdate="showUpdate"></Navbar>
        <AddForm v-if="addTask" :changeAddTask="changeAddTask"></AddForm>
        <UpdateForm :dataUpdate="dataUpdate" v-if="showUpdate" :changeUpdateTask="changeUpdateTask"></UpdateForm>
        <Home :updateTask='updateTask' v-if="!addTask && !showUpdate" :changeUpdateTask="changeUpdateTask"></Home>
        </div>
    </div>
    <LoginForm v-if="!isLogin && !showRegister" :changeRegister="changeRegister" :changeIsLogin="changeIsLogin"></LoginForm>
    <RegisterForm v-if="!isLogin && showRegister" :changeRegister="changeRegister"></RegisterForm>
    </div>
</template>

<script>
import Home from './views/Home.vue'
import Navbar from './components/Navbar.vue'
import LoginForm from './views/LoginForm.vue'
import RegisterForm from './views/RegisterForm.vue'
import AddForm from './views/AddForm.vue'
import UpdateForm from './views/UpdateForm.vue'

export default {  
    name: "App",
    data() {
        return {
            isLogin: false,
            showAdd: false,
            showRegister: false,
            addTask: false,
            showUpdate: false,
            dataUpdate: {}
        }
    },
    methods: {
        changeIsLogin(value) {
            this.isLogin = value
        },
        changeRegister(value) {
            this.showRegister = value
        },
        changeAddTask(value) {
            this.addTask = value
        },
        changeUpdateTask(value) {
            this.showUpdate = value
        },
        updateTask(data) {
            this.dataUpdate = data
            this.showUpdate = true
        }
    },
    components: {
        Navbar,
        Home,
        LoginForm,
        RegisterForm,
        AddForm,
        UpdateForm
    },
    created() {
        if(localStorage.access_token) {
            this.isLogin = true
        } else {
            this.isLogin = false
        }
    }
}
</script>

<style>
.background-style {
    background-image: url('https://images.unsplash.com/photo-1499750310107-5fef28a66643?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=750&q=80');
    background-repeat: no-repeat;
    background-size: cover;
    height: 680px;
}
</style>