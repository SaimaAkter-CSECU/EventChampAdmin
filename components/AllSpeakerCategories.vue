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
        name: 'AllSpeakerCategories',
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
                        cat: 'CEO',
                    },
                    {
                        id: 2,
                        cat: 'Founder',
                    },
                    {
                        id: 3,
                        cat: 'Model',
                    },
                    {
                        id: 4,
                        cat: 'Motivational Speaker',
                    },
                    {
                        id: 5,
                        cat: 'Designer',
                    },
                ],
            }
        },
        methods: {
            async goToCategoryDetail(){
                this.$nuxt.$router.push({path:'/Dashboard/Speakers/Category-Detail'});
            }
        }

    }
</script>