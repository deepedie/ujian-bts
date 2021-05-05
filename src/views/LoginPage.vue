<template>
  <v-container>
    <v-row>
      <v-col>
        <v-text-field v-model="username" label="Username" outline dense></v-text-field>
        <v-text-field v-model="password" label="Password" outline dense></v-text-field>
        <v-btn @click="login" dense blue>Submit</v-btn>
        <p>belum punya akun ? <router-link to="/register">Daftar</router-link></p>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import axios from 'axios'
const baseUrl = "http://18.139.50.74:8080"

export default {
  name: 'LoginPage',
  components: {
    // HelloWorld
  },
  data(){
    return{
      username: '',
      password: '',
      token: ''
    }
  },
  methods: {
    login(){
      axios.post(`${baseUrl}/login`, {
        username: this.username,
        password: this.password
      }).then(res => {
        console.log("hmm", res.data)
        this.token = res.data.data.token
        localStorage.setItem('token', res.data.data.token)
        this.$router.push( {name : "About"})
      }).catch(err => console.log(err))
    }
  }
}
</script>
