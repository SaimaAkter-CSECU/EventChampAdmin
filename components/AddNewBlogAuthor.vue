<template>
    <div>
        <div
            class="title-text mb-5"
        >
            Add New Author
        </div>
        <div>   
            <v-card class="pa-7">
                <v-form
                    ref="form"
                    v-model="valid"
                    lazy-validation
                >
                    <v-text-field
                        v-model="name"
                        :rules="inputRules"
                        label="Name"
                        outlined
                        required
                    ></v-text-field>

                    <client-only>
                        <vue-editor 
                            placeholder="Description..." 
                            v-model="description" 
                            required
                            class="mb-5"
                        ></vue-editor>
                    </client-only>

                    <v-text-field
                        v-model="fbLink"
                        label="Facebook Link"
                        outlined
                    ></v-text-field>

                    <v-text-field
                        v-model="instaLink"
                        label="Instagram Link"
                        outlined
                    ></v-text-field>

                    <v-text-field
                        v-model="twitterLink"
                        label="Twitter Link"
                        outlined
                    ></v-text-field>

                    <v-text-field
                        v-model="youtubeLink"
                        label="Youtube Link"
                        outlined
                    ></v-text-field>

                    <v-file-input
                        label="Author Image"
                        prepend-icon=""
                        prepend-inner-icon="mdi-camera"
                        outlined
                        required
                    ></v-file-input>

                    <v-btn
                        :disabled="!valid"
                        class="btn-style mr-4"
                        large
                        @click="addAuthor"
                        elevation="0"
                    >
                        Add User
                    </v-btn>

                    <v-btn
                        color="grey darken-2"
                        class="mr-4"
                        @click="reset"
                        large
                        elevation="0"
                    >
                        Cancel
                    </v-btn>
                </v-form>
            </v-card>        
        </div>

        <v-snackbar
            v-model="snackbar"
            timeout="2000"
            color="secondary"
        >
            {{snackbarText}}

            <template v-slot:action="{ attrs }">
                <v-btn
                    color="white"
                    text
                    v-bind="attrs"
                    @click="snackbar = false" 
                >
                Close
                </v-btn>
            </template>
        </v-snackbar>
    </div>
</template>

<script>
    export default {
        name: 'AddNewBlogAuthor',
        data: ()=>({
            valid: true,
            name: '',
            description: '', 
            fbLink: '',
            twitterLink: '',
            youtubeLink: '',
            instaLink: '',
            inputRules: [
                v => !!v || 'This field is required',
            ],
            snackbar: false,
            snackbarText: '' , 
        }),
        methods: {
            async addAuthor() {
                if(this.$refs.form.validate()){
                    this.snackbarText= 'Author Added Successfully';
                    this.snackbar= true; 
                    this.$refs.form.reset(); 
                }
            },
            async reset () {
                this.$refs.form.reset();
                this.$nuxt.$router.push({path:'/Dashboard/Blogs/All-Authors'})

            },
        },
    }
</script>