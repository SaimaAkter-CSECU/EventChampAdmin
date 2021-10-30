<template>
    <div>
        <div
            class="title-text mb-5"
        >
            All Users
        </div>
        <v-card>
            <v-card-title>
                <v-spacer></v-spacer>
                <v-text-field
                    v-model="search"
                    append-icon="mdi-magnify"
                    label="Search"
                    single-line
                    hide-details
                >
                </v-text-field>
            </v-card-title>
            <v-data-table
                :headers="headers"
                :items="users"
                :search="search"
                elevation="3"
                @click:row="goToUserDetail()"
                class="dataTable"
            ></v-data-table>
        </v-card>
    </div>
</template>

<script>
    export default {
        name: 'AllUsers',
        data () {
            return {
                search: '',
                headers:[
                    {
                        text: '#',
                        sortable: true,
                        value: 'id', 
                    },
                    {
                        text: 'UserName',
                        sortable: true,
                        value: 'username', 
                    },
                    {
                        text: 'Role',
                        sortable: true,
                        value: 'role', 
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
            }
        },
        methods: {
            async goToUserDetail(){
                this.$nuxt.$router.push({path:'/Dashboard/Users/User-Detail'});
            }
        }

    }
</script>