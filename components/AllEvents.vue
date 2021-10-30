<template>
    <div>
        <div
            class="title-text mb-5"
        >
            All Events
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
                :items="events"
                :search="search"
                elevation="3"
                @click:row="handleClick"
                class="dataTable"
            ></v-data-table>
        </v-card>
    </div>
</template>

<script>
    export default {
        name: 'AllEvents',
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
                        text: 'Event Title',
                        sortable: true,
                        value: 'title', 
                    },
                    {
                        text: 'Location',
                        sortable: true,
                        value: 'location', 
                    },
                    {
                        text: 'Date',
                        sortable: true,
                        value: 'date', 
                    },
                    {
                        text: 'Status',
                        sortable: true,
                        value: 'status', 
                    },
                    {
                        text: 'Category',
                        sortable: true,
                        value: 'category', 
                    },
                    {
                        text: 'Cost ($)',
                        sortable: false,
                        value: 'cost', 
                    },
                ],
                events: [
                    {
                        id: 1, 
                        title: 'Milano 21T Meeting', 
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        status: 'Showing', 
                        date: '21 November, 2021', 
                        location: 'Milano', 
                        catId: 2,
                        category: 'Business', 
                        cost: '29', 
                        url: require('../assets/Images/LatestPost/LatestPost1.png')
                    },
                    {
                        id: 2, 
                        title: 'Gaming X2021 Fair', 
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        status: 'Showing', 
                        date: '21 September, 2021', 
                        location: 'Istambul', 
                        catId: 11,
                        category: 'Technology', 
                        cost: '75', 
                        url: require('../assets/Images/LatestPost/LatestPost2.png')
                    },
                    {
                        id: 3, 
                        title: 'Eventchamp Conference', 
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        status: 'Showing', 
                        date: 'March 12, 2021', 
                        location: 'Istambul', 
                        catId: 2,
                        category: 'Business', 
                        cost: '149', 
                        url: require('../assets/Images/LatestPost/LatestPost3.png')
                    },
                    {
                        id: 4, 
                        title: 'The Future of Currencies', 
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        status: 'Showing', 
                        date: 'July 17, 2021', 
                        location: 'Milan', 
                        catId: 11,
                        category: 'Technology', 
                        cost: '299', 
                        url: require('../assets/Images/LatestPost/LatestPost4.png')
                    },
                    {
                        id: 5, 
                        title: 'Wedding of James & Helen',
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        status: 'Showing', 
                        date: 'August 20, 2021', 
                        location: 'California', 
                        catId: 13,
                        category: 'WEDDING', 
                        cost: 'Free', 
                        url: require('../assets/Images/LatestPost/LatestPost4.png')
                    },
                    {
                        id: 6, 
                        title: 'Travel Tour', 
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        status: 'Showing', 
                        date: '21 November, 2021', 
                        location: 'Milano', 
                        catId: 12,
                        category: 'Travel', 
                        cost: '29', 
                        url: require('../assets/Images/LatestPost/LatestPost1.png')
                    },
                    {
                        id: 7, 
                        title: 'Gaming X2021 Fair', 
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        status: 'Upcoming', 
                        date: '21 September, 2021', 
                        location: 'Istambul', 
                        catId: 10,
                        category: 'Sports', 
                        cost: '75', 
                        url: require('../assets/Images/LatestPost/LatestPost2.png')
                    },
                    {
                        id: 8, 
                        title: 'Eventchamp Party', 
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        status: 'Showing', 
                        date: 'March 12, 2021', 
                        location: 'Istambul', 
                        catId: 9,
                        category: 'Nightlife', 
                        cost: 'Free', 
                        url: require('../assets/Images/LatestPost/LatestPost3.png')
                    },
                    {
                        id: 9, 
                        title: 'The Future of Currencies', 
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        status: 'Expired', 
                        date: 'July 17, 2021', 
                        location: 'Milan', 
                        catId: 8,
                        category: 'Micellaneous', 
                        cost: '299', 
                        url: require('../assets/Images/LatestPost/LatestPost4.png')
                    },
                    {
                        id: 10, 
                        title: 'Wedding of James & Helen',
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        status: 'Expired', 
                        date: 'August 20, 2021', 
                        location: 'California', 
                        catId: 13,
                        category: 'WEDDING', 
                        cost: 'Free', 
                        url: require('../assets/Images/LatestPost/LatestPost4.png')
                    },
                    {
                        id: 11, 
                        title: 'Food carnival', 
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        status: 'Showing', 
                        date: '21 November, 2021', 
                        location: 'Milano', 
                        catId: 7,
                        category: 'Food', 
                        cost: '29', 
                        url: require('../assets/Images/LatestPost/LatestPost1.png')
                    },
                    {
                        id: 12, 
                        title: 'Gaming X2021 Fair', 
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        status: 'Upcoming', 
                        date: '21 September, 2021', 
                        location: 'Istambul', 
                        catId: 6,
                        category: 'Festival', 
                        cost: '75', 
                        url: require('../assets/Images/LatestPost/LatestPost2.png')
                    },
                    {
                        id: 13, 
                        title: 'Eventchamp Education', 
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        status: 'Showing', 
                        date: 'March 12, 2021', 
                        location: 'Istambul', 
                        catId: 5,
                        category: 'Education', 
                        cost: '149', 
                        url: require('../assets/Images/LatestPost/LatestPost3.png')
                    },
                    {
                        id: 14, 
                        title: 'The Future of Currencies', 
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        status: 'Showing', 
                        date: 'July 17, 2021', 
                        location: 'Milan', 
                        catId: 4,
                        category: 'Conferrence', 
                        cost: '299', 
                        url: require('../assets/Images/LatestPost/LatestPost4.png')
                    },
                    {
                        id: 15, 
                        title: 'Concert of James & Helen',
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        status: 'Expired', 
                        date: 'August 20, 2021', 
                        location: 'California', 
                        catId: 3,
                        category: 'Concert', 
                        cost: '75', 
                        url: require('../assets/Images/LatestPost/LatestPost4.png')
                    },
                    {
                        id: 16, 
                        title: 'Concert of James & Helen',
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        status: 'Expired', 
                        date: 'August 20, 2021', 
                        location: 'California', 
                        catId: 1,
                        category: 'Art', 
                        cost: '75', 
                        url: require('../assets/Images/LatestPost/LatestPost4.png')
                    },
                    {
                        id: 17, 
                        title: 'Drama Games 2021',
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        status: 'Upcoming', 
                        date: 'October 10, 2021', 
                        location: 'Helsink', 
                        catId: 1,
                        category: 'Art', 
                        cost: '39', 
                        url: require('../assets/Images/LatestPost/LatestPost4.png')
                    },
                ],
            }
        },
        methods: {
            async handleClick(){
                console.log("clicked")
            }
        }

    }
</script>