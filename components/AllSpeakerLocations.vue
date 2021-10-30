<template>
    <div>
        <div
            class="title-text mb-5"
        >
            All Locations
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
                :items="locations"
                :search="search"
                elevation="3"
                @click:row="goToLocationDetail()"
                class="dataTable"
            ></v-data-table>
        </v-card>
    </div>
</template>

<script>
    export default {
        name: 'AllSpeakerLocations',
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
                        text: 'Location',
                        sortable: true,
                        value: 'location', 
                    },                   
                ],
                locations:[
                    {
                        id: 1,
                        location: 'Romania',
                    },
                    {
                        id: 2,
                        location: 'Paris',
                    },
                    {
                        id: 3,
                        location: 'USA',
                    },
                    {
                        id: 4,
                        location: 'Istambul',
                    },
                    {
                        id: 5,
                        location: 'Dhaka',
                    },
                    {
                        id: 6,
                        location: 'Malaysia',
                    },
                ],
            }
        },
        methods: {
            async goToLocationDetail(){
                this.$nuxt.$router.push({path:'/Dashboard/Speakers/Location-Detail'});
            }
        }

    }
</script>