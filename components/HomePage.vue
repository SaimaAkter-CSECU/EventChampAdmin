<template>
    <div>
        <div v-show="loggedIn">
            <Header />
            <v-main>
                <v-container class="mb-9">
                    <Nuxt />
                </v-container>
            </v-main>
            <Footer />
        </div>
        <div v-show=!loggedIn> 
            <Login />
        </div>
    </div>
</template>

<script>
    export default {
        name: 'HomePage', 
        data: () =>({
            loggedIn: false,
        }), 
        mounted(){
            console.log(this.loggedIn);
            let user = localStorage.getItem('loggedIn');
            console.log(user);
            if(user){
                this.loggedIn = true;
            }
        }, 
    }
</script>