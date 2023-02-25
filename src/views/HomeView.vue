<template>
  <div class="home">
    <button class="btn btn-primary" v-if="!loggedIn" @click="loginWithGoogle">Googleでログイン</button>
    <button class="btn btn-primary" v-if="loggedIn" @click="logout">ログアウト</button>
    
    <hr>
    
    <img v-if="loggedIn" :src="userProfileImageUrl">
    <p v-if="loggedIn">{{ userDisplayName }}</p>
    
    <hr>

    <router-link to="/about"><button class="btn btn-primary">次のページへ</button></router-link>
  </div>

</template>

<script>
import "../assets/firebase.js"
import firebase from "firebase/app";
import 'firebase/auth';

export default {
  data() {
    return {
      loggedIn: false,
      userDisplayName: "",
      userProfileImageUrl: ""
    };
  },
  created() {
    firebase.auth().onAuthStateChanged((user) => {
      if (user) {
        this.userDisplayName = user.displayName;
        this.userProfileImageUrl = user.photoURL;
        this.loggedIn = true;
      } else {
        this.loggedIn = false;
      }
    });
  },
  methods: {
    async loginWithGoogle() {
      const provider = new firebase.auth.GoogleAuthProvider();
      try {
        const userCredential = await firebase.auth().signInWithPopup(provider);
        const user = userCredential.user;

        // ログイン情報をローカルストレージに保存する
        localStorage.setItem('currentUser', JSON.stringify(user));

      } catch (error) {
        alert(error)
      }
    },
    async logout() {
      await firebase.auth().signOut();
    },
  }
}
</script>
