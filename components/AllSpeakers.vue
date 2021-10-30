<template>
    <div>
        <div
            class="title-text mb-5"
        >
            All Speakers
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
                :items="speakers"
                :search="search"
                elevation="3"
                @click:row="goToSpeakerDetail()"
                class="dataTable"
            ></v-data-table>
        </v-card>
    </div>
</template>

<script>
    export default {
        name: 'AllSpeakers',
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
                        text: 'Name',
                        sortable: true,
                        value: 'name', 
                    },
                    {
                        text: 'Email',
                        sortable: true,
                        value: 'email', 
                    },
                    {
                        text: 'Phone',
                        sortable: true,
                        value: 'phone', 
                    },
                    {
                        text: 'Category',
                        sortable: true,
                        value: 'category', 
                    },
                    {
                        text: 'Location',
                        sortable: true,
                        value: 'location', 
                    },
                ],
                speakers: [
                    {
                        id: 1, 
                        name: 'Speaker 1', 
                        email: 'speaker1@gmail.com', 
                        phone: '01234567891',
                        category: 'CEO',
                        location: 'Istambul'
                    },
                    {
                        id: 2, 
                        name: 'Speaker 2', 
                        email: 'speaker2@gmail.com', 
                        phone: '01234567892',
                        category: 'Designer',
                        location: 'France'
                    },
                    {
                        id: 3, 
                        name: 'Speaker 3', 
                        email: 'speaker3@gmail.com', 
                        phone: '01234567893',
                        category: 'Founder',
                        location: 'USA'
                    },
                    {
                        id: 4, 
                        name: 'Speaker 4', 
                        email: 'speaker4@gmail.com', 
                        phone: '01234567894',
                        category: 'CEO',
                        location: 'Istambul'
                    },
                    {
                        id: 5, 
                        name: 'Speaker 5', 
                        email: 'speaker5@gmail.com', 
                        phone: '01234567895',
                        category: 'Designer',
                        location: 'England'
                    },
                    {
                        id: 6, 
                        name: 'Speaker 6', 
                        email: 'speaker6@gmail.com', 
                        phone: '01234567896',
                        category: 'Model',
                        location: 'Paris'
                    },
                    {
                        id: 7, 
                        name: 'Speaker 7', 
                        email: 'speaker7@gmail.com', 
                        phone: '01234567897',
                        category: 'Model',
                        location: 'USA'
                    },
                    {
                        id: 8, 
                        name: 'Speaker 8', 
                        email: 'speaker8@gmail.com', 
                        phone: '01234567892',
                        category: 'Motivational Speaker',
                        location: 'USA' 
                    },
                    {
                        id: 9, 
                        name: 'Speaker 9', 
                        email: 'speaker9@gmail.com', 
                        phone: '01234567899',
                        category: 'CEO',
                        location: 'USA' 
                    },
                    {
                        id: 10, 
                        name: 'Speaker 10', 
                        email: 'speaker10@gmail.com', 
                        phone: '01234567890',
                        category: 'Model',
                        location: 'Australia' 
                    },
                ],
            }
        },
        methods: {
            async goToSpeakerDetail(){
                this.$nuxt.$router.push({path:'/Dashboard/Speakers/Speaker-Detail'});
            }
        }

    }
</script>