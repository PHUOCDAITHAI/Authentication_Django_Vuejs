<template>
    <div class="login">
        <h1>Log In</h1>
        <form @submit.prevent="submitForm">
            <input type="text" v-model="username">
            <input type="password" v-model="password">
            <button type="submit">Log in</button>
        </form>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'Login',
    data(){
        return {
            username: '',
            password: ''
        }
    },
    methods: {
        submitForm(){
            const formData = {
                username: this.username,
                password:  this.password
            }
            axios.post('token/login', formData)
            .then(res => {
                console.log(res);
                const token  = res.data.auth_token
                this.$store.commit('setToken', token)
                axios.defaults.headers.common['Authorization'] = 'Token ' + token
                localStorage.setItem('token', token)
            })
            .catch(error => console.log(error))
        }
    }
}
</script>

<style>

</style>