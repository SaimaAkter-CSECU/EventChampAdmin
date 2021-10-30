<template>
    <div>
        <div
            class="title-text mb-5"
        >
            Add New User
        </div>
        <div>           
            <v-form
                ref="form"
                v-model="valid"
                lazy-validation
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
                    label="Password"
                    type="password"
                    outlined
                    required
                ></v-text-field>

                <v-select
                    v-model="userType"
                    :items="userTypes"
                    item-text="type"
                    item-value="id"
                    :rules="[v => !!v || 'Item is required']"
                    label="User Type"
                    outlined
                    required
                ></v-select>

                <v-btn
                    :disabled="!valid"
                    class="btn-style mr-4"
                    large
                    @click="addUser"
                    elevation="0"
                >
                    Add User
                </v-btn>

                <v-btn
                    color="grey darken-2"
                    class="mr-4"
                    @click="reset"
                    large
                    elevation="0"
                >
                    Cancel
                </v-btn>
            </v-form>
        </div>

        <v-snackbar
            v-model="snackbar"
            timeout="2000"
            color="secondary"
        >
            {{snackbarText}}

            <template v-slot:action="{ attrs }">
                <v-btn
                    color="white"
                    text
                    v-bind="attrs"
                    @click="snackbar = false" 
                >
                Close
                </v-btn>
            </template>
        </v-snackbar>
    </div>
</template>

<script>
    export default {
        name: 'AddNewUser',
        data: ()=>({
            valid: true,
            username: '',
            password: '',
            inputRules: [
                v => !!v || 'Name is required',
            ],
            userType: null,
            userTypes: [
                {
                    id: 1,
                    type: 'Admin',
                },
                {
                    id: 2,
                    type: 'Normal User',
                },
            ],
            users: [
                {
                    id: 1, 
                    username: 'Saima', 
                    role: 'Admin', 
                },
                {
                    id: 2, 
                    username: 'Saima 2', 
                    role: 'Normal User', 
                },
                {
                    id: 3, 
                    username: 'Test User',  
                    role: 'Normal User', 
                },
                {
                    id: 4, 
                    username: 'Test User 2',  
                    role: 'Normal User', 
                },
                {
                    id: 5, 
                    username: 'Test User 3', 
                    role: 'Normal User', 
                },
                {
                    id: 6, 
                    username: 'Test User 4',  
                    role: 'Normal User', 
                },
                {
                    id: 7, 
                    username: 'Test User 5',  
                    role: 'Normal User', 
                },
                {
                    id: 8, 
                    username: 'Admin3', 
                    role: 'Admin', 
                },
                {
                    id: 9, 
                    username: 'Admin4', 
                    role: 'Admin', 
                },
                {
                    id: 10, 
                    username: 'Admin5',  
                    role: 'Admin', 
                },
            ],
            snackbar: false,
            snackbarText: '' , 
        }),
        methods: {
            addUser() {
                if(this.$refs.form.validate()){
                    let user = this.users.find(x=> x.username == this.username);
                    if(user){
                        this.snackbarText= 'User Already Exist';
                        this.snackbar= true; 
                    }
                    else{
                        this.snackbarText= 'User Added Successfully';
                        this.snackbar= true; 
                        this.$refs.form.reset(); 
                    }
                }
            },
            reset () {
                this.$refs.form.reset()
            },
        },
    }
</script>