<template>
    <div>
        <div
            class="title-text mb-5"
        >
            All Blogs
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
                :items="blogs"
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
        name: 'AllBlogs', 
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
                        text: 'Date',
                        sortable: true,
                        value: 'date', 
                    },
                ],
                blogs: [
                    {
                        id: '1',
                        title: 'Top 20 Event and Conference Country',
                        category: 'lists',
                        date: 'November 23, 2018',
                        url: require('../assets/Images/Blog/blog1.png'),
                    }, 
                    {
                        id: '2',
                        title: 'Budgets for Business Events',
                        category: 'News',
                        date: 'November 23, 2018',
                        url: require('../assets/Images/Blog/blog2.png'),
                    }, 
                    {
                        id: '3',
                        title: '5 Ideas for Fun Family Activities',
                        category: 'Lists',
                        date: 'November 23, 2018',
                        url: require('../assets/Images/Blog/blog1.png'),
                    }, 
                    {
                        id: '4',
                        title: 'Best Event Ticket Deals',
                        category: 'events',
                        date: 'November 23, 2018',
                        url: require('../assets/Images/Blog/blog2.png'),
                    }, 
                    {
                        id: '5',
                        title: 'Video Equipments for Events',
                        category: 'Events',
                        date: 'November 23, 2018',
                        url: require('../assets/Images/Blog/blog1.png'),
                    }, 
                    {
                        id: '6',
                        title: 'Best Event Musics',
                        category: 'Culture',
                        date: 'November 23, 2018',
                        url: require('../assets/Images/Blog/blog2.png'),
                    }, 
                    {
                        id: '7',
                        title: 'Top 20 Event and Conference Countries 2 xdtcfyvg tcyvgubh',
                        category: 'Lists',
                        date: 'November 23, 2018',
                        url: require('../assets/Images/Blog/blog1.png'),
                    }, 
                ],
            }
        },
        methods: {
            async goToBlogDetail(){
                this.$nuxt.$router.push({path:'/Dashboard/Blogs/Blog-Detail'});
            }
        }

    }
</script>