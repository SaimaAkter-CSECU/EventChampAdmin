<template>
    <div>
        <div
            class="title-text mb-5"
        >
            Speaker Detail
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
                            md="4"
                            sm="6"
                            xs="12"
                        >
                            <v-img
                                :src="viewProfilePicture"
                            ></v-img>
                        </v-col>
                        <v-col
                            col="12"
                            md="8"
                            sm="6"
                            xs="12"
                        >
                            <v-card-title class="text-h5 pt-0">{{viewName}}</v-card-title>
                            <v-card-subtitle class="pb-1 subtitle-1">{{viewCategory}}</v-card-subtitle>
                            <v-card-subtitle class="pt-1 subtitle-1">
                                {{viewShortDescription}}
                            </v-card-subtitle>
                            <div class="text-p pl-4 black--text">
                                <div class="pb-2">
                                    Location: {{viewLocation}}
                                </div>
                                <div class="pb-2">
                                    Address: {{viewAddress}}
                                </div>
                                <div class="pb-2">
                                    Phone: {{viewPhone}}
                                </div>
                                <div class="pb-2">
                                    Email: {{viewEmail}}
                                </div>
                                <div class="pb-2">
                                    Website: {{viewWebsiteLink}}
                                </div>
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
                    <v-row
                        class="mb-5 mt-5"
                    >
                        <v-col
                            col="12"
                            md="12"
                            sm="12"
                            xs="12"
                            style="border-bottom: 1px solid #eaeaea"
                            class="text-h5"
                        >
                            Description
                        </v-col>
                        <v-col
                            col="12"
                            xs="12"
                        >
                            <v-img
                                :src="viewBannerImage"
                                max-height="800px"
                                class="mb-5"
                            ></v-img>
                            <div v-html="viewDescription"></div>
                        </v-col>
                    </v-row>

                    <v-row
                        class="mb-5"
                    >
                        <v-col
                            col="12"
                            md="12"
                            sm="12"
                            xs="12"
                            style="border-bottom: 1px solid #eaeaea"
                            class="text-h5 mb-5"
                        >
                            Photos
                        </v-col>
                        <v-col
                            col="12"
                            xs="12"
                        >
                            <v-row>
                                <v-col
                                    col="12"
                                    md="4"
                                    sm="6"
                                    xs="12"
                                    class="pa-0"
                                    v-for="viewPhoto in viewPhotos"
                                    :key="viewPhoto.id"
                                >
                                    <v-img
                                        :src="viewPhoto.url"
                                    ></v-img>
                                </v-col>
                            </v-row>
                        </v-col>
                    </v-row>

                    <v-row
                        class="mb-5"
                    >
                        <v-col
                            col="12"
                            md="12"
                            sm="12"
                            xs="12"
                            style="border-bottom: 1px solid #eaeaea"
                            class="text-h5 "
                        >
                            Tags
                        </v-col>
                        <v-col
                            col="12"
                            xs="12"
                        >
                            <v-row>
                                <v-col
                                    col="12"
                                    md="12"
                                    sm="12"
                                    xs="12"
                                    class="d-flex align-center flex-wrap"
                                >
                                    <div
                                        v-for="tag in viewTags"
                                        :key="tag.id"
                                        
                                    >
                                        <v-btn
                                            elevation="2"
                                            color="grey darken-1"
                                            class="white--text mr-3 my-2"
                                            style="cursor: default"
                                        >
                                            {{tag.tag}}
                                        </v-btn>
                                    </div>
                                </v-col>
                            </v-row>
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
                        label="Speaker Id"
                        outlined
                        required
                        readonly
                    ></v-text-field>

                    <v-text-field
                        v-model="name"
                        :rules="inputRules"
                        label="Speaker Name"
                        outlined
                        required
                    ></v-text-field>

                    <v-select
                        v-model="category"
                        :items="categories"
                        item-value="catId"
                        item-text="cat"
                        :rules="inputRules"
                        label="Category/Designation"
                        outlined
                        required
                    ></v-select>

                    <v-textarea
                        v-model="shortDescription"
                        :rules="inputRules"
                        label="Short Description"
                        row="3"
                        outlined
                        required
                    ></v-textarea>

                    <v-file-input 
                        v-model="profilePicture"
                        label="Speaker Image"
                        prepend-icon=""
                        outlined
                    >
                    </v-file-input>

                    <v-select
                        v-model="location"
                        :items="locations"
                        item-value="id"
                        item-text="location"
                        :rules="inputRules"
                        label="Location"
                        outlined
                        required
                    ></v-select>

                    <v-text-field
                        v-model="address"
                        :rules="inputRules"
                        label="Address"
                        outlined
                        required
                    ></v-text-field>

                    <v-text-field
                        v-model="phone"
                        :rules="inputRules"
                        label="Speaker Phone"
                        outlined
                        required
                    ></v-text-field>

                    <v-text-field
                        v-model="email"
                        :rules="inputRules"
                        label="Speaker Email"
                        outlined
                        required
                    ></v-text-field>

                    <v-text-field
                        v-model="websiteLink"
                        label="Website Link"
                        outlined
                    ></v-text-field>

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

                    <client-only>
                        <vue-editor 
                            placeholder="Speaker Description... " 
                            v-model="description" 
                            required
                            class="mb-9"
                        ></vue-editor>
                    </client-only>

                    <v-file-input 
                        v-model="photos"
                        chips
                        label="Photos"
                        prepend-icon=""
                        multiple
                        outlined
                    >
                    </v-file-input>

                    <v-select
                        v-model="tags"
                        :items="allTags"
                        item-text="tag"
                        item-value="id"
                        chips
                        label="Tags"
                        multiple
                        class="my-5"
                        outlined
                    ></v-select>


                    <v-btn
                        :disabled="!valid"
                        class="btn-style mr-4"
                        large
                        @click="UpdateSpeakerInfo"
                        elevation="0"
                    >
                        Update Speaker Info
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

    let VueEditor;
    if (process.browser) {
        VueEditor = require('vue2-editor').VueEditor
    }

    export default {
        name: 'SpeakerDetail', 
        data:()=>({
            viewMode: true,
            speaker:[
                {
                    id: 3,
                    name: 'Ece Demir',
                    catId: 3, 
                    category: 'Journalist',
                    locId: 4,
                    location: 'Izmir',
                    address: 'Walking Street, 39531, New York, United States',
                    shortDescription: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad ne nec dolore oblique nusquam.',
                    phone: '1324567879809',
                    email: 'dctrfgyhuj@gmail.com',
                    websiteLink: 'http://www.speaker.com',
                    facebookLink: 'http://www.facebook.com',
                    twitterLink: 'http://twitter.com',
                    instagramLink: 'http://instagram.com',
                    youtubeLink: 'http://youtube.com',
                    bannerImage: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/speaker-photo-2-1130x650.jpg',
                    description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has. Sed ad dicam platonem, mea eros illum elitr id, ei has similique constituto. Ea movet saperet rationibus sit, pri autem aliquip invidunt an. Consetetur omittantur consequuntur eos et. <strong> Eleifend praesent iudicabit no mea, tollit persequeris ex pri, tota splendide voluptaria in pri.</strong> Ad per tale aliquip, ei sit viris commune albucius. Eos aliquip scaevola ut, eum alii mentitum prodesset no, his ne suas atomorum. Et numquam deleniti ponderum vis, quod error at mei. Novum blandit adolescens sea te. Ea eum cetero scaevola.<br /><br />In his meis porro viris, illud imperdiet reprimique et vim. Feugiat atomorum reprehendunt vix ei, ei facete regione pri. Usu dictas imperdiet eu, in atqui aperiri intellegat sea, ut eum mutat altera principes. Te sit quaeque oportere, has modus inani ceteros ad. Impedit blandit deseruisse duo ea, ne graecis deleniti incorrupte usu. Ut mei splendide accommodare. An pri iisque meliore, eam ei splendide eloquentiam philosophia. <u>Ne per meis eleifend electram.</u> Ne eam porro aliquam invidunt. Minim docendi eloquentiam cum ad. Quo ea mazim ubique, ex est fuisset blandit scaevola. Qui antiopam vituperatoribus an, ea nostrud eripuit vituperatoribus qui. In eam diam nominati, per ea alia luptatum. <span class="yellowish--text">Nam habemus electram democritum ut.</span> Mei ea omnium admodum intellegat. Habeo atqui molestiae at mei, an nec ridens consequuntur. Quem nulla cum ei, his ipsum apeirian no, per at eius iriure aperiri. Sed dicam interesset ei. Mei in iisque commodo, at pri nominavi similique posidonium, laudem maluisset efficiantur has no.<br/><br /><br />His verterem consectetuer consequuntur ne, no virtute atomorum usu. <b> Eu quo nemore causae tacimates, eos viderer persequeris an.</b> Cu molestie consulatu qui. Natum labores perfecto no ius, pri dico mundi inciderint id. Ei usu dico libris postea. Cu graeco doctus splendide qui, ei eum probo regione.', 
                    profilePicture: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/speaker-4-350x350.jpg', 
                    photos: [
                        {
                            id: 1,
                            url: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/speaker-photos-4.jpg',
                        },
                        {
                            id: 2,
                            url: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/speaker-photos-4.jpg',
                        },
                        {
                            id: 3,
                            url: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/speaker-photos-4.jpg',
                        },
                        {
                            id: 4,
                            url: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/speaker-photos-4.jpg',
                        },
                        {
                            id: 5,
                            url: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/speaker-photos-4.jpg',
                        },
                        {
                            id: 6,
                            url: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/speaker-photos-4.jpg',
                        },
                        {
                            id: 7,
                            url: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/speaker-photos-4.jpg',
                        },
                        {
                            id: 8,
                            url: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/speaker-photos-4.jpg',
                        },
                        {
                            id: 9,
                            url: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/speaker-photos-4.jpg',
                        }
                    ], 
                    tags:[
                        {
                            id: 1, 
                            tag: 'Speaker', 
                        },
                        {
                            id: 2, 
                            tag: 'Conferrence', 
                        },
                        {
                            id: 3, 
                            tag: 'Meeting', 
                        },
                        {
                            id: 4, 
                            tag: 'Culture', 
                        },
                        {
                            id: 5, 
                            tag: 'Art', 
                        },
                        {
                            id: 6, 
                            tag: 'Event', 
                        }
                    ]
                }
            ],
            categories: [
                {
                    id: 1,
                    cat: 'CEO',
                },
                {
                    id: 2,
                    cat: 'Founder',
                },
                {
                    id: 3,
                    cat: 'Model',
                },
                {
                    id: 4,
                    cat: 'Motivational Speaker',
                },
                {
                    id: 5,
                    cat: 'Designer',
                },
            ],
            locations:[
                {
                    id: 1,
                    location: 'Romania',
                },
                {
                    id: 2,
                    location: 'Paris',
                },
                {
                    id: 3,
                    location: 'USA',
                },
                {
                    id: 4,
                    location: 'Istambul',
                },
                {
                    id: 5,
                    location: 'Dhaka',
                },
                {
                    id: 6,
                    location: 'Malaysia',
                },
            ],
            allTags:[
                    {
                        id: 1,
                        tag: 'Business',
                    },
                    {
                        id: 2,
                        tag: 'Conferrence',
                    },
                    {
                        id: 3,
                        tag: 'Speakers',
                    },
                    {
                        id: 4,
                        tag: 'Event',
                    },
                    {
                        id: 5,
                        tag: 'Storyteller',
                    },
                    {
                        id: 6,
                        tag: 'Food',
                    },
                    {
                        id: 7,
                        tag: 'Meeting',
                    }
            ],
            viewName: '',
            viewCategory: '',
            viewLocation: '',
            viewAddress: '',
            viewShortDescription: '',
            viewPhone: '',
            viewEmail: '',
            viewWebsiteLink: '',
            viewFacebookLink: '',
            viewTwitterLink: '',
            viewInstagramLink: '',
            viewYoutubeLink: '',
            viewDescription: '',
            viewProfilePicture: '', 
            viewBannerImage: '',
            viewPhotos: [], 
            viewTags: [], 

            id: '',
            name: '',
            category: {},
            location: {},
            address: '',
            shortDescription: '',
            phone: '',
            email: '',
            websiteLink: '',
            facebookLink: '',
            twitterLink: '',
            instagramLink: '',
            youtubeLink: '',
            description: '',
            bannerImage: '',
            profilePicture: null,
            photos: [],
            tags: [],

            url: null, 
            
            snackbar: false,
            snackbarText: '' ,
            valid: true,
            
            inputRules: [
                v => !!v || 'This Field is Required',
            ],
            

        }),
        methods: {
            async UpdateSpeakerInfo(){
                if(this.$refs.form.validate()){
                    this.snackbarText= 'Speaker Info Updated Successfully';
                    this.snackbar= true; 
                    this.viewMode= true; 
                }
            },
            async reset(){
                this.$nuxt.$router.push({path: '/Dashboard/Speakers/All-Speakers'})
            },
            // async Preview_image() {
            //     this.url= URL.createObjectURL(this.profilePicture)
            // },
        },
        mounted() {
            this.id = this.speaker[0].id; 

            this.viewName = this.speaker[0].name;
            this.viewCategory = this.speaker[0].category;
            this.viewLocation = this.speaker[0].location;
            this.viewAddress = this.speaker[0].address;
            this.viewShortDescription = this.speaker[0].shortDescription;
            this.viewPhone = this.speaker[0].phone;
            this.viewEmail = this.speaker[0].email;
            this.viewWebsiteLink = this.speaker[0].websiteLink;
            this.viewFacebookLink = this.speaker[0].facebookLink;
            this.viewTwitterLink = this.speaker[0].twitterLink;
            this.viewInstagramLink = this.speaker[0].instagramLink;
            this.viewYoutubeLink = this.speaker[0].youtubeLink;
            this.viewDescription = this.speaker[0].description;
            this.viewBannerImage =  this.speaker[0].bannerImage;
            this.viewProfilePicture = this.speaker[0].profilePicture;
            this.viewPhotos = this.speaker[0].photos;
            this.viewTags = this.speaker[0].tags;

            this.name = this.speaker[0].name;
            this.category = { id: this.speaker[0].catId, cat: this.speaker[0].category };
            this.location = { id: this.speaker[0].locId, location: this.speaker[0].location };
            // this.location = this.speaker[0].location;
            this.address = this.speaker[0].address;
            this.shortDescription = this.speaker[0].shortDescription;
            this.phone = this.speaker[0].phone;
            this.email = this.speaker[0].email;
            this.websiteLink = this.speaker[0].websiteLink;
            this.facebookLink = this.speaker[0].facebookLink;
            this.twitterLink = this.speaker[0].twitterLink;
            this.instagramLink = this.speaker[0].instagramLink;
            this.youtubeLink = this.speaker[0].youtubeLink;
            this.description = this.speaker[0].description;
            this.bannerImage =  this.speaker[0].bannerImage;
            // this.profilePicture = this.speaker[0].profilePicture;
            // this.photos = this.speaker[0].photos;
            this.tags = this.speaker[0].tags;
        }
    }
</script>