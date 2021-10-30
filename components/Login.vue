<template>
    <div>
        <div
            color="grey lighten-4"
            class="w-100"
            style="height: 100vh;"
        >
            <div
                class="d-flex align-center flex-column justify-center w-100 h-100"
                background-color="grey lighten-4"
            >
                <div>
                <div
                    class="mb-5 w-100"
                >
                    <v-img
                    :src="logo"
                    width="250px"
                    class="mx-auto"
                    ></v-img>
                </div>
                <v-card
                    min-width="350px"
                    elevation="5"
                >
                    <v-form
                    ref="form"
                    v-model="valid"
                    lazy-validation
                    class="pa-7"
                    >
                    <v-text-field
                        v-model="username"
                        :rules="inputRules"
                        label="Username"
                        outlined
                        required
                    ></v-text-field>

                    <v-text-field
                        v-model="password"
                        :rules="inputRules"
                        type="password"
                        label="Password"
                        required
                        outlined
                    ></v-text-field>

                    <v-btn
                        :disabled="!valid"
                        class="d-block btn-style "
                        elevation="0"
                        large
                        block
                        @click="login"
                    >
                        Login
                    </v-btn>

                    </v-form>

                </v-card>
                </div>
            </div>
        </div>

        <v-snackbar
            v-model="loginSnackbar"
            timeout="2000"
            color="secondary"
        >
            {{loginSnackbarText}}

            <template v-slot:action="{ attrs }">
                <v-btn
                    color="white"
                    text
                    v-bind="attrs"
                    @click="loginSnackbar = false" 
                >
                Close
                </v-btn>
            </template>
        </v-snackbar>
    </div>
</template>

<script>
    import logo from '../assets/Images/logo.png' 
    export default {
        name: 'Login', 
        data: ()=>({
            logo: logo,
            password: '',
            username: '', 
            inputRules: [
                v => !!v || 'This field is required',
            ],
            valid: true, 
            users:[
                {
                    id: 1,
                    username: 'Saima',
                    password: 'Saima', 
                },
                {
                    id: 2,
                    username: 'Sovon',
                    password: 'Sovon', 
                },
            ],
            loginSnackbar: false,
            loginSnackbarText: '', 
            loggedIn: false, 
        }),
        methods:{
            async login() {
                if(this.$refs.form.validate()){
                    let user = this.users.find(x=> x.username == this.username && x.password == this.password);
                    if(user){
                        this.loginSnackbarText = 'Login Successfully!'; 
                        this.loginSnackbar = true; 
                        localStorage.setItem("loggedIn", 'true'); 
                        this.loggedIn= true; 
                        // this.$nuxt.$router.push('/'); 
                    }
                    else{
                        this.loginSnackbarText = 'Credential Error!'; 
                        this.loginSnackbar = true; 
                    }
                }
            },
        },
        mounted() {
            let user = localStorage.getItem("loggedIn"); 
            console.log(user);
            if(user){
                this.$nuxt.$router.push('/Dashboard/Events/All-Events'); 
            }
        },
    }
</script>