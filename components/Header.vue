<template>
    <div>
        <v-navigation-drawer
            v-model="drawer"
            fixed
            app
            dark
        >
            <v-list
            >
                <!-- <v-list-item  
                    class="mt-5 d-flex justify-center"
                >
                    <v-list-item-avatar 
                        class="ma-0" 
                        width="40%" 
                        height="auto"
                    >
                        <v-img
                            :src="logo"
                            alt="Nextive Solution"
                            class="img-fluid aff-logo"
                        >
                        </v-img>
                    </v-list-item-avatar>
                </v-list-item>    -->
                <v-list-item  
                    class="text-center"
                >
                    <h3 class="font-weight-regular mx-auto">BD Events</h3>
                </v-list-item>   
                <v-divider style="color: #fb0" class="mb-7"></v-divider>

                <div 
                    v-for="item in items" 
                    :key="item.name" 
                    class="headerNav"
                    router
                    exact
                >
                    <v-list-item
                        color="white"
                    >
                        <v-list-group>
                            <v-list-item slot='activator'>
                                <v-list-item-icon class="mr-1">
                                    <v-icon>{{ item.icon }}</v-icon>
                                </v-list-item-icon>
                                <v-list-item-title 
                                    class="menuTitle"
                                >
                                    {{ item.name }}
                                </v-list-item-title>
                            </v-list-item>
                            <v-list-item 
                                v-for='sub in item.subLinks' 
                                :key="sub.name" 
                                class="ms-5 mainNav" 
                                router :to="sub.path"
                            >
                                <v-list-item-title>
                                    {{ sub.title }}
                                </v-list-item-title>
                            </v-list-item>
                        </v-list-group>
                    </v-list-item>
                </div>
            </v-list>
        </v-navigation-drawer>

        <v-app-bar
            :clipped-left="clipped"
            fixed
            app
            dark
        >
            <v-app-bar-nav-icon @click.stop="drawer = !drawer" /> 
            <v-toolbar-title class="ml-5 white--text">Dashboard</v-toolbar-title>

            <v-spacer></v-spacer>
            <v-btn
                @click="logOut"
                color="secondary"
            >
                Logout
            </v-btn>
        </v-app-bar>
        
    </div>
</template>

<script>
    export default {
        name: 'Header',
        data() {
            return {
                clipped: false,
                drawer: true,
                fixed: false,
                items: [
                    {
                        id: 1, 
                        icon: "mdi-calendar-text-outline",
                        name: "Events",
                        subLinks: [
                            {
                                id: 1, 
                                title: 'All Events', 
                                path: '/Dashboard/Events/All-Events', 
                            },
                            {
                                id: 2, 
                                title: 'Add New Event', 
                                path: '/Dashboard/Events/Add-New-Event', 
                            },
                            {
                                id: 3, 
                                title: 'All Pending Events', 
                                path: 'Dashboard/Pending-Events', 
                            },
                            {
                                id: 4, 
                                title: 'All Event Categories', 
                                path: 'Dashboard/Event-Categories', 
                            },
                            {
                                id: 5, 
                                title: 'Add New Event Category', 
                                path: 'Dashboard/Add-Event-Category', 
                            },
                            {
                                id: 6, 
                                title: 'All Event Locations', 
                                path: 'Dashboard/Event-Locations', 
                            },
                            {
                                id: 7, 
                                title: 'Add New Event Location', 
                                path: 'Dashboard/Add-Event-Location', 
                            },
                            {
                                id: 8, 
                                title: 'All Event Organizers', 
                                path: 'Dashboard/Event-Organizers', 
                            },
                            {
                                id: 9, 
                                title: 'Add New Event Organizer', 
                                path: 'Dashboard/Add-Event-Organizer', 
                            },
                            {
                                id: 10, 
                                title: 'All Event Tags', 
                                path: 'Dashboard/Event-Tags', 
                            },
                            {
                                id: 11, 
                                title: 'Add New Event Tag', 
                                path: 'Dashboard/Add-Event-Tag', 
                            },
                        ], 
                    },
                    {
                        id: 2, 
                        icon: "mdi-map-legend",
                        name: "Venues",
                        subLinks: [
                            {
                                id: 1, 
                                title: 'All Venues', 
                                path: '/Dashboard/Venues/All-Venues', 
                            },
                            {
                                id: 2, 
                                title: 'Add New Venue', 
                                path: '/Dashboard/Venues/Add-New-Venue', 
                            },
                            {
                                id: 3, 
                                title: 'All Venue Categories', 
                                path: '/Dashboard/Venues/All-Categories', 
                            },
                            {
                                id: 4, 
                                title: 'Add New Venue Category', 
                                path: '/Dashboard/Venues/Add-New-Category', 
                            },
                            {
                                id: 5, 
                                title: 'All Venue Locations', 
                                path: '/Dashboard/Venues/All-Locations', 
                            },
                            {
                                id: 6, 
                                title: 'Add New Venue Location', 
                                path: '/Dashboard/Venues/Add-New-Location', 
                            },
                            {
                                id: 7, 
                                title: 'All Venue Tags', 
                                path: '/Dashboard/Venues/All-Tags', 
                            },
                            {
                                id: 8, 
                                title: 'Add New Venue Tag', 
                                path: '/Dashboard/Venues/Add-New-Tag', 
                            },
                        ], 
                    },
                    {
                        id: 3, 
                        icon: "mdi-view-grid-outline",
                        name: "Blogs",
                        subLinks: [
                            {
                                id: 1, 
                                title: 'All Blogs', 
                                path: '/Dashboard/Blogs/All-Blogs', 
                            },
                            {
                                id: 2, 
                                title: 'Add New Blog', 
                                path: '/Dashboard/Blogs/Add-New-Blog', 
                            },
                            {
                                id: 3, 
                                title: 'All Pending Blogs', 
                                path: '/Dashboard/Blogs/All-Pending-blogs', 
                            },
                            {
                                id: 4, 
                                title: 'All Blog Categories', 
                                path: '/Dashboard/Blogs/All-Categories', 
                            },
                            {
                                id: 5, 
                                title: 'Add New Blog Category', 
                                path: '/Dashboard/Blogs/Add-New-Category', 
                            },
                            {
                                id: 6, 
                                title: 'All Blog Locations', 
                                path: '/Dashboard/Blogs/All-Locations', 
                            },
                            {
                                id: 7, 
                                title: 'Add New Blog Location', 
                                path: '/Dashboard/Blogs/Add-New-Location', 
                            },
                            {
                                id: 8, 
                                title: 'All Blog Tags', 
                                path: '/Dashboard/Blogs/All-Tags', 
                            },
                            {
                                id: 9, 
                                title: 'Add New Blog Tag', 
                                path: '/Dashboard/Blogs/Add-New-Tag', 
                            },
                            {
                                id: 10, 
                                title: 'All Blog Authors', 
                                path: '/Dashboard/Blogs/All-Authors', 
                            },
                            {
                                id: 11, 
                                title: 'Add New Blog Author', 
                                path: '/Dashboard/Blogs/Add-New-Author', 
                            },
                        ], 
                    },
                    {
                        id: 4, 
                        icon: "mdi-account-circle-outline",
                        name: "Speakers",
                        subLinks: [
                            {
                                id: 1, 
                                title: 'All Speakers', 
                                path: '/Dashboard/Speakers/All-Speakers', 
                            },
                            {
                                id: 2, 
                                title: 'Add New Speaker', 
                                path: '/Dashboard/Speakers/Add-New-Speaker', 
                            },
                            {
                                id: 3, 
                                title: 'All Speaker Locations', 
                                path: '/Dashboard/Speakers/All-Locations', 
                            },
                            {
                                id: 4, 
                                title: 'Add New Speaker Location', 
                                path: '/Dashboard/Speakers/Add-New-Location', 
                            },
                            {
                                id: 5, 
                                title: 'All Speaker Categories', 
                                path: '/Dashboard/Speakers/All-Categories', 
                            },
                            {
                                id: 6, 
                                title: 'Add New Speaker Category', 
                                path: '/Dashboard/Speakers/Add-New-Category', 
                            },
                            {
                                id: 7, 
                                title: 'All Speaker Tags', 
                                path: '/Dashboard/Speakers/All-Tags', 
                            },
                            {
                                id: 8, 
                                title: 'Add New Speaker Tag', 
                                path: '/Dashboard/Speakers/Add-New-Tag', 
                            },
                        ], 
                    },
                    {
                        id: 5, 
                        icon: "mdi-account-group-outline",
                        name: "Users",
                        subLinks: [
                            {
                                id: 1, 
                                title: 'All Users', 
                                path: 'Dashboard/Users', 
                            },
                            {
                                id: 2, 
                                title: 'Add New User', 
                                path: 'Dashboard/Add-New-User', 
                            },
                        ], 
                    },
                    
                ],
            }
        },
        methods: {
            async logOut(){
                localStorage.setItem("loggedIn", false);
                this.$nuxt.$router.push({path:'/'})
            }
        },
    }
</script>