<template>
    <div>
        <div
            class="title-text mb-5"
        >
            User Detail
        </div>
        <v-card
            elevation="3"
        >
            <v-card-title>
                <v-spacer></v-spacer>
                <v-btn
                    class="ml-3"
                    color="primary"
                    v-show="viewMode"
                    @click="viewMode = false"
                >
                    Edit
                </v-btn>
                <v-btn
                    class="ml-3"
                    color="grey darken-2"
                    v-show="!viewMode"
                    @click="viewMode = true"
                >
                    Cancel
                </v-btn>
            </v-card-title>
            <div
                v-if="viewMode"
                class="pa-7"
            >
                <v-row>
                    <v-col
                        col="12"
                        md="4"
                        sm="6"
                        xs="12"
                    >
                        <v-list-item two-line>
                            <v-list-item-content>
                                <v-list-item-title class="text-h6 font-weight-regular">Username</v-list-item-title>
                                <v-list-item-subtitle class="subtitle-1 mt-2">{{viewUsername}}</v-list-item-subtitle>
                            </v-list-item-content>
                        </v-list-item>
                    </v-col>
                    <v-col
                        col="12"
                        md="4"
                        sm="6"
                        xs="12"
                    >
                        <v-list-item two-line>
                            <v-list-item-content>
                                <v-list-item-title class="text-h6 font-weight-regular">Password</v-list-item-title>
                                <v-list-item-subtitle class="subtitle-1 mt-2">{{viewPassword}}</v-list-item-subtitle>
                            </v-list-item-content>
                        </v-list-item>
                    </v-col>
                    <v-col
                        col="12"
                        md="4"
                        sm="6"
                        xs="12"
                    >
                        <v-list-item two-line>
                            <v-list-item-content>
                                <v-list-item-title class="text-h6 font-weight-regular">User Type</v-list-item-title>
                                <v-list-item-subtitle class="subtitle-1 mt-2">{{viewUserType}}</v-list-item-subtitle>
                            </v-list-item-content>
                        </v-list-item>
                    </v-col>

                </v-row>
            </div>
            <div
                v-else
                class="pa-7"
            >
                <v-form
                    ref="form"
                    v-model="valid"
                    lazy-validation
                >
                    <v-text-field
                        v-model="id"
                        :rules="inputRules"
                        label="User Id"
                        outlined
                        required
                        readonly
                    ></v-text-field>

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
                        @click="UpdateUserInfo"
                        elevation="0"
                    >
                        Update User Info
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
        </v-card>

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
        name: 'UserDetail',
        data:()=>({
            viewMode: true,
            user:[
                {
                    id: 2,
                    username: 'Saima2345',
                    password: 'ctfvvgbh',
                    userTypeId: '2', 
                    userType: 'Admin', 
                }
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
            snackbar: false,
            snackbarText: '' ,
            valid: true,
            id: '',
            username: '',
            password: '',
            inputRules: [
                v => !!v || 'Name is required',
            ],
            viewUsername: '',
            viewPassword: '', 
            viewUserType: '', 

        }),
        methods: {
            async UpdateUserInfo(){
                if(this.$refs.form.validate()){
                    this.snackbarText= 'User Info Updated Successfully';
                    this.snackbar= true;  
                }
            },
            async reset(){
                // this.$refs.form.reset(); 
                this.$nuxt.$router.push({path: '/Dashboard/Users/All-Users'})
            }
        },
        mounted() {
            this.id = this.user[0].id; 
            this.username = this.user[0].username;
            this.viewUsername = this.user[0].username;
            this.password = this.user[0].password;
            this.viewPassword = this.user[0].password;
            this.viewUserType = this.user[0].userType;
            this.userType = {
                id: this.user[0].userTypeId,
                type: this.user[0].userType,
            }
            
        }
    }
</script>