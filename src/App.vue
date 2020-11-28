<template>
  <div id="app">
    <amplify-authenticator>
      <div>
        <h1>Hey, {{ user.username }}!</h1>
        <amplify-sign-out></amplify-sign-out>
      </div>
    </amplify-authenticator>
  </div>
</template>

<script>
import { AuthState, onAuthUIStateChange } from '@aws-amplify/ui-components';
// import { Auth } from 'aws-amplify';

export default {
  name: 'App',
  data() {
    return {
      user: {}
    };
  },
  created() {
    // authentication state managament
    onAuthUIStateChange((state, user) => {
      // set current user and load data after login
      if (state === AuthState.SignedIn) {
        this.user = user;
      }

      /* Auth.currentAuthenticatedUser().then(res => {
        console.log(res);
      }); */
    });
  }
};
</script>

<style></style>
