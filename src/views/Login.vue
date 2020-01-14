<template>
    <div id="login">
        <h1>Login Page</h1>
        <div id="input">
        <input type="text" name="email" v-model="input.email" placeholder="Email" />
         </div>
         <div id="input">
        <input type="password" name="password" v-model="input.password" placeholder="Password" />
        </div>
        <button type="button" v-on:click="login()">Login</button>
        <div id="message" v-if="showMessage">
             Please enter a valid email and password!!
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Login',
        data() {
            return {
                input: {
                    email: "",
                    password: ""
                },
                showMessage : false
            }
        },
        methods: {
            login() {
                this.$http.post("https://reqres.in/api/login", {
                    email: this.input.email,
                    password: this.input.password
                }).then(function(data){
                    console.log(data);
                    this.$emit("authenticated", true);
                    this.$router.replace({ name: "dashboard" });
                }).catch(function(error){
                    this.showMessage = true;
                    console.log(error);
                });
            }
        }
    }
</script>

<style scoped>
    #login {
        width: 500px;
        height: 160px;
        border: 1px solid #CCCCCC;
        background-color: #FFFFFF;
        margin: auto;
        margin-top: 200px;
        padding: 20px;
    }
    #input {
        padding: 10px;
    }
    button {
        float: right;
    }
    #message {
        color: red;
        padding-left: 10px;
    }
</style>