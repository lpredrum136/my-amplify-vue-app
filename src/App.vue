<template>
  <div id="app">
    <!-- <amplify-authenticator>
      <div>
        <h1>Hey, {{ user.username }}!</h1>
        <amplify-sign-out></amplify-sign-out>
      </div>
    </amplify-authenticator> -->

    <!--SIGN IN-->
    <form @submit="onSubmit">
      <input type="text" name="username" id="username" v-model="username" />
      <input type="password" name="password" id="password" v-model="password" />
      <input type="submit" value="Login" />
    </form>
    <button @click="logout">Sign outttt</button>

    <!--GET DATA VIA API-->
    <button @click="getCustomers">Get all customerssss</button>
  </div>
</template>

<script>
// import { AuthState, onAuthUIStateChange } from '@aws-amplify/ui-components';
import { Auth, API } from 'aws-amplify';

export default {
  name: 'App',
  data() {
    return {
      user: {},
      username: '',
      password: ''
    };
  },
  created() {
    // authentication state managament
    /* onAuthUIStateChange((state, user) => {
      // set current user and load data after login
      if (state === AuthState.SignedIn) {
        this.user = user;
      }
    }); */
    this.checkAuth();
  },

  methods: {
    onSubmit(event) {
      event.preventDefault();
      // console.log(this.username, this.password);
      this.login();
    },

    async login() {
      try {
        const user = await Auth.signIn({
          username: this.username,
          password: this.password
        });
        console.log(user);
      } catch (error) {
        console.log('error signing in: ', error);
      }
    },
    async logout() {
      try {
        await Auth.signOut();
        console.log('Sign out successfully');
      } catch (error) {
        console.log('error signing out: ', error);
      }
    },
    async checkAuth() {
      console.log('checking auth');
      try {
        const user = await Auth.currentAuthenticatedUser();
        console.log('Authenticated user: ', user);
      } catch (error) {
        console.log('User not logged in', error);
      }
    },
    async getCustomers() {
      const apiName = 'customerAPI';
      const path = '/customers';
      const init = {};
      // optional
      /* const init = {
        headers: {

        },
        response: true,
        queryStringParameters: {
          name: 'param'
        }
      } */

      try {
        const res = await API.get(apiName, path, init);
        console.log(res.success);
      } catch (error) {
        console.log(error.response);
      }
    }
  }
};
</script>

<style></style>
