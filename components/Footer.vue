<template>
    <v-footer
      dark
      :absolute="!fixed"
      app
    >
      <span class="w-100 d-flex justify-end">&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
</template>

<script>
    export default {
        name: 'Footer',
        data: ()=>({
            fixed: true,
        }), 
    }
</script> 