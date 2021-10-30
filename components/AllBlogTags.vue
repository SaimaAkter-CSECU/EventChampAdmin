<template>
    <div>
        <div
            class="title-text mb-5"
        >
            All Tags
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
                :items="tags"
                :search="search"
                elevation="3"
                @click:row="goToTagDetail()"
                class="dataTable"
            ></v-data-table>
        </v-card>
    </div>
</template>

<script>
    export default {
        name: 'AllBlogTags',
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
                        text: 'Tag',
                        sortable: true,
                        value: 'tag', 
                    },                   
                ],
                tags:[
                    {
                        id: 1,
                        tag: 'Business',
                    },
                    {
                        id: 2,
                        tag: 'Conferrence',
                    },
                    {
                        id: 3,
                        tag: 'Speakers',
                    },
                    {
                        id: 4,
                        tag: 'Event',
                    },
                    {
                        id: 5,
                        tag: 'Storyteller',
                    },
                    {
                        id: 6,
                        tag: 'Food',
                    },
                    {
                        id: 7,
                        tag: 'Meeting',
                    }
                ],
            }
        },
        methods: {
            async goToTagDetail(){
                this.$nuxt.$router.push({path:'/Dashboard/Blogs/Tag-Detail'});
            }
        }

    }
</script>