<template>
    <div>
        <div
            class="title-text mb-5"
        >
            Author Detail
        </div>
        <v-card
            elevation="3"
        >
            <v-card-title>
                <v-spacer></v-spacer>
                <v-btn
                    class="ml-3"
                    color="primary"
                    v-show="viewMode"
                    @click="viewMode = false"
                >
                    Edit
                </v-btn>
                <v-btn
                    class="ml-3"
                    color="grey darken-2"
                    v-show="!viewMode"
                    @click="viewMode = true"
                >
                    Cancel
                </v-btn>
            </v-card-title>
            <div
                v-if="viewMode"
                class="pa-7"
            >
                <v-card
                    elevation="0"
                >
                    <v-row
                    >
                        <v-col
                            col="12"
                            md="3"
                            sm="4"
                            xs="12"
                        >
                            <v-img
                                :src="viewProfilePicture"
                                class="rounded-lg"
                            ></v-img>
                        </v-col>
                        <v-col
                            col="12"
                            md="9"
                            sm="8"
                            xs="12"
                        >
                            <v-card-title class="text-h5 pt-0">{{viewName}}</v-card-title>
                            <v-card-subtitle class="pt-1 subtitle-1">
                                {{viewDescription}}
                            </v-card-subtitle>
                            <div class="text-p pl-4 black--text">
                                <div class="pb-2">
                                    Facebook: {{viewFacebookLink}}
                                </div>
                                <div class="pb-2">
                                    Twitter: {{viewTwitterLink}}
                                </div>
                                <div class="pb-2">
                                    Instagram: {{viewInstagramLink}}
                                </div>
                                <div class="pb-2">
                                    Youtube: {{viewYoutubeLink}}
                                </div>
                            </div>
                        </v-col>
                    </v-row>
                </v-card>
            </div>
            <div
                v-else
                class="pa-7"
            >
                <v-form
                    ref="form"
                    v-model="valid"
                    lazy-validation
                >
                    <v-text-field
                        v-model="id"
                        :rules="inputRules"
                        label="Author Id"
                        outlined
                        required
                        readonly
                    ></v-text-field>

                    <v-text-field
                        v-model="name"
                        :rules="inputRules"
                        label="Author Name"
                        outlined
                        required
                    ></v-text-field>

                    <v-textarea
                        v-model="description"
                        :rules="inputRules"
                        label="Author Description"
                        row="3"
                        outlined
                        required
                    ></v-textarea>

                    <v-text-field
                        v-model="facebookLink"
                        label="Facebook Link"
                        outlined
                    ></v-text-field>

                    <v-text-field
                        v-model="twitterLink"
                        label="Twitter Link"
                        outlined
                    ></v-text-field>

                    <v-text-field
                        v-model="instagramLink"
                        label="Instagram Link"
                        outlined
                    ></v-text-field>

                    <v-text-field
                        v-model="youtubeLink"
                        label="Youtube Link"
                        outlined
                    ></v-text-field>

                    <v-file-input 
                        v-model="profilePicture"
                        label="Author Image"
                        prepend-icon=""
                        outlined
                    >
                    </v-file-input>

                    <v-btn
                        :disabled="!valid"
                        class="btn-style mr-4"
                        large
                        @click="UpdateAuthorInfo"
                        elevation="0"
                    >
                        Update Author Info
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
            </div>
        </v-card>

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
        name: 'BlogAuthorDetail', 
        data:()=>({
            viewMode: true,
            
            authors: [
                {
                    id: 1, 
                    name: 'Author 1', 
                    description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                    facebookLink: 'www.facebook.com',
                    twitterLink: 'www.twitter.com',
                    instagramLink: 'www.instagram.com',
                    youtubeLink: 'www.youtube.com',
                    profilePicture: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/avatar-150x150.jpg', 
                },
            ],
            viewName: '',
            viewDescription: '',
            viewFacebookLink: '',
            viewTwitterLink: '',
            viewInstagramLink: '',
            viewYoutubeLink: '',
            viewProfilePicture: '', 
            

            id: '',
            name: '',
            description: '',
            facebookLink: '',
            twitterLink: '',
            instagramLink: '',
            youtubeLink: '',
            profilePicture: null,
            
            snackbar: false,
            snackbarText: '' ,
            valid: true,
            
            inputRules: [
                v => !!v || 'This Field is Required',
            ],
            

        }),
        methods: {
            async UpdateAuthorInfo(){
                if(this.$refs.form.validate()){
                    this.snackbarText= 'Author Info Updated Successfully';
                    this.snackbar= true; 
                    this.viewMode= true; 
                }
            },
            async reset(){
                this.$nuxt.$router.push({path: '/Dashboard/Blogs/All-Authors'})
            },
            // async Preview_image() {
            //     this.url= URL.createObjectURL(this.profilePicture)
            // },
        },
        mounted() {
            this.id = this.authors[0].id; 

            this.viewName = this.authors[0].name;
            this.viewDescription = this.authors[0].description;
            this.viewFacebookLink = this.authors[0].facebookLink;
            this.viewTwitterLink = this.authors[0].twitterLink;
            this.viewInstagramLink = this.authors[0].instagramLink;
            this.viewYoutubeLink = this.authors[0].youtubeLink;
            this.viewProfilePicture = this.authors[0].profilePicture;

            this.name = this.authors[0].name;
            this.description = this.authors[0].description;
            this.facebookLink = this.authors[0].facebookLink;
            this.twitterLink = this.authors[0].twitterLink;
            this.instagramLink = this.authors[0].instagramLink;
            this.youtubeLink = this.authors[0].youtubeLink;
            // this.profilePicture = this.authors[0].profilePicture;
        }
    }
</script>