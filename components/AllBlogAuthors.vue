<template>
    <div>
        <div
            class="title-text mb-5"
        >
            All Blog Authors
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
                :items="authors"
                :search="search"
                elevation="3"
                @click:row="goToAuthorDetail()"
                class="dataTable"
            ></v-data-table>
        </v-card>
    </div>
</template>

<script>
    export default {
        name: 'AllBlogAuthors',
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
                        text: 'No of Blog Posted',
                        sortable: true,
                        value: 'count', 
                    },
                ],
                authors: [
                    {
                        id: 1, 
                        name: 'Author 1', 
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        facebookLink: 'www.facebook.com',
                        twitterLink: 'www.twitter.com',
                        instagramLink: 'www.instagram.com',
                        youtubeLink: 'www.youtube.com',
                        count: 1,
                    },
                    {
                        id: 2, 
                        name: 'Author 2', 
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        facebookLink: 'www.facebook.com',
                        twitterLink: 'www.twitter.com',
                        instagramLink: 'www.instagram.com',
                        youtubeLink: 'www.youtube.com',
                        count: 1,
                    },
                    {
                        id: 3, 
                        name: 'Author 3', 
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        facebookLink: 'www.facebook.com',
                        twitterLink: 'www.twitter.com',
                        instagramLink: 'www.instagram.com',
                        youtubeLink: 'www.youtube.com',
                        count: 2,
                    },
                    {
                        id: 4, 
                        name: 'Author 4', 
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        facebookLink: 'www.facebook.com',
                        twitterLink: 'www.twitter.com',
                        instagramLink: 'www.instagram.com',
                        youtubeLink: 'www.youtube.com',
                        count: 1,
                    },
                    {
                        id: 5, 
                        name: 'Author 5', 
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        facebookLink: 'www.facebook.com',
                        twitterLink: 'www.twitter.com',
                        instagramLink: 'www.instagram.com',
                        youtubeLink: 'www.youtube.com',
                        count: 2,
                    },
                    {
                        id: 6, 
                        name: 'Author 6', 
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        facebookLink: 'www.facebook.com',
                        twitterLink: 'www.twitter.com',
                        instagramLink: 'www.instagram.com',
                        youtubeLink: 'www.youtube.com',
                        count: 1,
                    },
                    {
                        id: 7, 
                        name: 'Author 7', 
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        facebookLink: 'www.facebook.com',
                        twitterLink: 'www.twitter.com',
                        instagramLink: 'www.instagram.com',
                        youtubeLink: 'www.youtube.com',
                        count: 4,
                    },
                    {
                        id: 8, 
                        name: 'Author 8', 
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        facebookLink: 'www.facebook.com',
                        twitterLink: 'www.twitter.com',
                        instagramLink: 'www.instagram.com',
                        youtubeLink: 'www.youtube.com',
                        count: 1,
                    },
                    {
                        id: 9, 
                        name: 'Author 9',
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        facebookLink: 'www.facebook.com',
                        twitterLink: 'www.twitter.com',
                        instagramLink: 'www.instagram.com',
                        youtubeLink: 'www.youtube.com',
                        count: 1,
                    },
                    {
                        id: 10, 
                        name: 'Author 10', 
                        description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                        facebookLink: 'www.facebook.com',
                        twitterLink: 'www.twitter.com',
                        instagramLink: 'www.instagram.com',
                        youtubeLink: 'www.youtube.com',
                        count: 3,
                    },
                ],
            }
        },
        methods: {
            async goToAuthorDetail(){
                this.$nuxt.$router.push({path:'/Dashboard/Blogs/Author-Detail'});
            }
        }

    }
</script>