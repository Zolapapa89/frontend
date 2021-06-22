<template>

<div id="login">


    <div id="formDiv" class="panel">
       
        <div id="titleDiv"><h2 id="title"> Login </h2></div>

        <form v-on:submit.prevent="submit()">

            <label class="label" for="user">User</label>
            <input class="input" type="text" v-model="form.user">

            <label class="label" for="password">Password</label>
            <input class="input" type="password" v-model="form.password">

            <p id="errorM">{{errorMessage}}</p>

            <button id="submitButton" class="button is-primary">Login</button>
                
        </form>

    </div>

    
</div>

</template>

<script>

import axios from 'axios'

export default {
    data(){
        return {
            form: {
                user: '',
                password: ''
            },
            errorMessage: ""
        }
    },

    methods: {
        submit(){
            
            axios.post('https://otthoni-feladat-backend.herokuapp.com/login', this.form)
                .then(function( response ){
                    console.log(response);
                    console.log(response.data.token);
                    const token = response.data.token;
                    localStorage.setItem('user-token', token) // store the token in localstorage
                    //console.log(token);
                    window.location.href = '/data';
                    }).catch(function (error) {
                    console.log(error)
                    localStorage.removeItem('user-token')
                    this.errorMessage = "Hibás felhasználónév vagy jelszó!"
                    }.bind(this));
        }
    }
}

</script>
<style>

#login {
    height: 90%;
     display: flex;
    align-items: center;
    justify-content: center;
    vertical-align: center;
}
#titleDiv{
    width: 100%;
    height: 80px;
    display: flex;
    align-items: center;
    justify-content: center;
    padding-bottom: 5px;
   
}
#title {
    
    width: 90%;
    text-align: center;
    font-size: 30px;
    font-weight: bold;
  
}
#formDiv {
    width: 50%;
    display: flex;
    flex-direction: column;
    align-items: center;
}
form {
    width: 90%;
    padding: 10px;
    
}
#submitButton{
    margin-top: 20px;
    margin-bottom: 20px;
}
#errorM{
    margin-top: 10px;
    color: red;
}

</style>