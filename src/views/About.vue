<template>
  <div class="about">
    <h1>{{users}}</h1>
  </div>
</template>
<script>
import axios from 'axios';

export default {
  
    data(){
        return {
            users: []
        }
    },



    // Component data, methods, etc.
    methods: {
    loadUsers(){
      const token = localStorage.getItem('user-token')
      console.log(token)
  // GET request using axios with set headers
  const headers = {"x-api-key": token};
        axios.get("https://otthoni-feladat-backend.herokuapp.com/data", { headers })
            .then(function( response ){
                this.users = response.data;
                console.log(response.data)
            }.bind(this));
    }
}
}
</script>
