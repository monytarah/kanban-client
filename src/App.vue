<template>
    <div>
    <Navbar :isLogin="isLogin" :changeIsLogin="changeIsLogin" :changeAddTask="changeAddTask" :showUpdate="showUpdate"></Navbar>
    <LoginForm v-if="!isLogin && !showRegister" :changeRegister="changeRegister" :changeIsLogin="changeIsLogin"></LoginForm>
    <RegisterForm v-if="!isLogin && showRegister" :changeRegister="changeRegister"></RegisterForm>
    <AddForm v-if="isLogin && addTask" :changeAddTask="changeAddTask"></AddForm>
    <UpdateForm :dataUpdate="dataUpdate" v-if="isLogin && showUpdate" :changeUpdateTask="changeUpdateTask"></UpdateForm>
    <Home :updateTask='updateTask'  v-if="isLogin && !addTask && !showUpdate" :changeUpdateTask="changeUpdateTask"></Home>
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

</style>