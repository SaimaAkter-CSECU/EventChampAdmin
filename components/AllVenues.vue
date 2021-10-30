<template>
    <div>
        <div
            class="title-text mb-5"
        >
            All Venues
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
                :items="venues"
                :search="search"
                elevation="3"
                @click:row="goToBlogDetail()"
                class="dataTable"
            ></v-data-table>
        </v-card>
    </div>
</template>

<script>
    export default {
        name: 'AllVenues', 
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
                        text: 'Title',
                        sortable: true,
                        value: 'title', 
                    },
                    {
                        text: 'Location',
                        sortable: true,
                        value: 'location', 
                    },
                    {
                        text: 'Category',
                        sortable: true,
                        value: 'category', 
                    },
                ],
                venues: [
                {
                    id: 1,
                    title: 'Tokyo Meeting Center',
                    category: 'Meeting', 
                    location: 'Tokyo', 
                    
                },
                {
                    id: 2,
                    title: 'London Arena',
                    category: 'Wedding', 
                    location: 'London', 
                },
                {
                    id: 3,
                    title: 'Istanbul Event Arena',
                    category: 'Conferrence', 
                    location: 'Istambul',
                },
                {
                    id: 4,
                    title: 'Best Event Ticket Deals',
                    category: 'Concert', 
                    location: 'Tokyo',
                },
                {
                    id: 5,
                    title: 'Love Wedding Hall',
                    category: 'Wedding', 
                    location: 'Tokyo', 
                },
                {
                    id: 6,
                    title: 'Oxnard Beach',
                    category: 'Party', 
                    location: 'Australia',
                }
            ],
            }
        },
        methods: {
            async goToBlogDetail(){
                this.$nuxt.$router.push({path:'/Dashboard/Venues/Venue-Detail'});
            }
        }

    }
</script>