<template>
    <div class="Signup">
        <h1>Sign up</h1>
        <form @submit.prevent="submitForm">
            <input type="text" v-model="username">
            <input type="email" v-model="email">
            <input type="password" v-model="password">
            <button type="submit">Sign up</button>
        </form>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'SignUp',
    data(){
        return {
            username: '',
            password: '',
            email: ''
        }
    },
    methods: {
        submitForm(){
            const formData = {
                username: this.username,
                password: this.password,
                email: this.email
            }
            axios.post('users/', formData)
            .then(res => {
                this.$router.push('/login')
                console.log(res);
            })
            .catch(error => console.log(error))
        }
    }
}
</script>

<style>

</style>