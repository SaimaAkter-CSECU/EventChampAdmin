<template>
  <div v-show="!loggedIn">
    <Login />
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
                this.loggedIn = false; 
                this.$nuxt.$router.push({path:'/'})
            }
        },
    }
</script>

