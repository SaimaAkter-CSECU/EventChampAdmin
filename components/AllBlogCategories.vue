<template>
    <div>
        <div
            class="title-text mb-5"
        >
            All Categories
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
                :items="categories"
                :search="search"
                elevation="3"
                @click:row="goToCategoryDetail()"
                class="dataTable"
            ></v-data-table>
        </v-card>
    </div>
</template>

<script>
    export default {
        name: 'AllBlogCategories',
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
                        text: 'Category',
                        sortable: true,
                        value: 'cat', 
                    },                   
                ],
                categories: [
                    {
                        id: 1, 
                        cat: 'Art', 
                    },
                    {
                        id: 2, 
                        cat: 'Business', 
                    },
                    {
                        id: 3, 
                        cat: 'Concert', 
                    },
                    {
                        id: 4, 
                        cat: 'Conferrence', 
                    },
                    {
                        id: 5, 
                        cat: 'Education', 
                    },
                    {
                        id: 6, 
                        cat: 'Festival', 
                    },
                    {
                        id: 7, 
                        cat: 'Food', 
                    },
                    {
                        id: 8, 
                        cat: 'Micellaneous', 
                    },
                    {
                        id: 9, 
                        cat: 'Nightlife', 
                    },
                    {
                        id: 10, 
                        cat: 'Sports', 
                    },
                    {
                        id: 11, 
                        cat: 'Technology', 
                    },
                    {
                        id: 12, 
                        cat: 'Travel', 
                    },
                    {
                        id: 13, 
                        cat: 'Wedding', 
                    },
                ],
            }
        },
        methods: {
            async goToCategoryDetail(){
                this.$nuxt.$router.push({path:'/Dashboard/Blogs/Category-Detail'});
            }
        }

    }
</script>