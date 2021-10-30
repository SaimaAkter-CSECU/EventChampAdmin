<template>
    <div>
        <Header />
        <v-main>
            <v-container>
                rdtfyghj dctrfgyhuj xdctfvgbun xdctfvgbuhnj dashboard
            </v-container>
        </v-main>
        <Footer />
    </div>
</template>

<script>
    export default {
        data() {
            return {
                loggedIn: true,
            }
        },
        mounted() {
            let user = localStorage.getItem("loggedIn");
            if(user){
                this.$nuxt.$router.push({path:'/Dashboard/Events/All-Events'}); 
            }
            else{
                this.$nuxt.$router.push({path:'/'})
            }
        },
    }
</script>

