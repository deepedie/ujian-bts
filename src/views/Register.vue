<template>
  <v-container>
    <v-row>
      <v-col>
        <v-text-field v-model="email" label="Email" outline dense></v-text-field>
        <v-text-field v-model="username" label="Username" outline dense></v-text-field>
        <v-text-field v-model="password" label="Password" outline dense></v-text-field>
        <v-btn @click="Register" dense blue>Register</v-btn>
        <p>{{message}} <router-link to="/">Login</router-link></p>
        <p></p>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from 'axios'
const baseUrl = "http://18.139.50.74:8080"

export default {
  name: 'LoginPage',
  components: {
    // HelloWorld
  },
  data(){
    return{
        email: '',
        username: '',
        password: '',
        token: '',
        message: 'Login Sekarang',
    }
  },
  methods: {
    Register(){
      axios.post(`${baseUrl}/register`, {
        email: this.email,
        username: this.username,
        password: this.password
      }).then(res => {
        console.log("hmm", res.data)
        this.message = res.data.message
        this.email = ''
        this.username = ''
        this.password = ''
      }).catch(err => console.log(err))
    }
  }
}
</script>
