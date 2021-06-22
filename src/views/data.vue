<template>

<div id="dataDiv" class="columns is-centered is-vcentered">
           
    <div >
        <table class="table is-bordered is-striped is-narrow is-vcentered">
            <thead>
                <tr>
                    <th>id</th>
                    <th>text</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>{{users[0].id}}</td>
                    <td>{{users[0].text}}</td>
                </tr>
                <tr>
                    <td>{{users[1].id}}</td>
                    <td>{{users[1].text}}</td>
                </tr>
            </tbody>
        </table>
        
    </div>

    <div>
        <button id="logoutButton" class="button is-dark is-outlined" v-on:click="logout()">Logout</button>
    </div>

</div>
    
</template>
<script>

import axios from 'axios';

export default {
  
    data(){
        return {
            users: [],
        }
    },



    methods: {
        loadUsers(){
            const token = localStorage.getItem('user-token')
        
            const headers = {"x-api-key": token};
             
            axios.get("https://otthoni-feladat-backend.herokuapp.com/data", { headers })
                .then(function( response ){
                this.users = response.data;                                        
                }.bind(this));
      
        },
        logout(){
            localStorage.removeItem('user-token')
            window.location.href = '/'
        }
    },
    created: function(){
 
        this.loadUsers()
    }
}

</script>
<style>

    html, body {
        height: 100%;
    }
    #app {
        height: 100%;
    }
    #dataDiv {
        height: 90%;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }
    table {
        height: 20%;
    }
    #logoutButton {
        margin-top: 20px;
    }
    
</style>