<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> |
      <button @click="topArtists()">top artists</button> |
      <button @click="topTracks()">top songs</button>
    </div>
    <router-view/>
  </div>
</template>


<script lang="ts">
import Vue from 'vue';
import Component from 'vue-class-component';
const axios = require('axios');
      function getHashParams() {
          var hashParams = {};
          var e, r = /([^&;=]+)=?([^&;]*)/g,
              q = window.location.hash.substring(1);
          while ( e = r.exec(q)) {
             hashParams[e[1]] = decodeURIComponent(e[2]);
          }
          return hashParams;
        }
  var params = getHashParams();
        var accessToken = params.access_token

@Component({
  props: {
    propMessage: String,
  },
})
export default class App extends Vue {
  topArtists() {
    // Make a request for a user with a given ID
    axios.get('https://api.spotify.com/v1/me/top/artists?time_range=short_term&limit=10', {
      headers: { 'Authorization': 'Bearer ' + accessToken },
    })
      .then((response: any) => {
        // handle success
        console.log(response.data);
      })
      .catch((error: any) => {
        // handle error
        console.log(error);
      });
  }
    topTracks() {
    // Make a request for a user with a given ID
    axios.get('https://api.spotify.com/v1/me/top/tracks?time_range=short_term&limit=10', {
      headers: { 'Authorization': 'Bearer ' + accessToken },
    })
      .then((response: any) => {
        // handle success
        console.log(response.data);
      })
      .catch((error: any) => {
        // handle error
        console.log(error);
      });
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
