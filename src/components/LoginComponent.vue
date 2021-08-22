<template>
    <div>
        <h1> Please login to play RPS</h1>
        <form class="loginForm">
            <input type="text" id="email" placeholder="Email" v-model="user.email">
            <input type="text" id="password" placeholder="Password" v-model="user.password" >
            <input id="submit" type="submit" value="Login" @click="login">
            <p id="warningMessage">Something is wrong. Please try again</p>
        </form>
    </div>
</template>

<script>
import router from '../router';
import cookies from 'vue-cookies';
import axios from 'axios';

export default {
  name: "LoginComponent",
    data() {
      return {
        user: {
          email: "",
          password: ""
        }
      }
    },
    methods: {
      login: function() {
        axios.request({
          method: "POST",
          url: "https://reqres.in/api/login",
          headers: {
            "Content-type": "application/json"
          },
          data: {
            email: this.user.email,
            password: this.user.password
          }
        }).then((response) => {
            cookies.set('userToken', response.data.token);
            router.push('/game');
        }).catch((error) => {
            console.log(error);
            document.getElementById('warningMessage').style.display = 'block';
        })
    },

    }
}
</script>

<style scoped>
  #warningMessage {
    color: red;
    display: none;
    font-size: 2em;
  }
  h1{
      margin-bottom: 40px;
  }
  .loginForm input{
    display: block;
    text-align: center;
    margin: 15px auto;
    font-size: 1.6em;
    padding: 5px 20px ;
  }

  #submit {
    padding: 5px 25px ;
  }
</style>