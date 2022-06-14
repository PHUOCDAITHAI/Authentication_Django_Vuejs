<template>
  <nav>
    <router-link to="/signup">Sign Up</router-link> |
    
    <div v-if="isAuthenticated">
      <button @click="removeToken">Logout</button>
    </div>
    <div v-else>
      <router-link to="/login">Log In</router-link>
      Not Auth
    </div>
  </nav>
  <router-view/>
</template>
<script>
import axios from 'axios'
import { mapState, mapMutations } from 'vuex'
export default {
  name: 'App',
  computed: {
    ...mapState(['isAuthenticated'])
  },
  methods: {
    ...mapMutations(['removeToken'])
  },
  beforeCreate(){
    this.$store.commit('initializeStore')
    const token = this.$store.state.token
    if(token){
      axios.defaults.headers.common['Authorization'] = "Token " + token
    }else {
      axios.defaults.headers.common['Authorization'] = ''
    }
  },
  
}
</script>
<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
