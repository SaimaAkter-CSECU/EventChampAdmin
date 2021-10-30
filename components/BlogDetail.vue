<template>
    <div>
        <div
            class="title-text mb-5"
        >
            Blog Detail
        </div>
        <v-card
            elevation="3"
        >
            <v-card-title>
                <v-spacer></v-spacer>
                <div
                    v-show="viewMode"
                >
                    <v-btn
                        class="ml-3"
                        color="primary"
                        v-show="statusId == '1' "
                        @click="viewMode = false"
                    >
                        Edit
                    </v-btn>
                    <v-btn
                        class="ml-3"
                        color="success"
                        v-show ="statusId == 2"
                        @click="approveBlog(), statusId = 1"
                    >
                        Approve Blog
                    </v-btn>
                </div>
                
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
                            md="12"
                            sm="12"
                            xs="12"
                        >
                            <v-card-title class="text-h4 pt-0 pb-4">{{viewTitle}}</v-card-title>
                            <v-card-subtitle class="py-1 subtitle-1">
                                {{viewShortDescription}}
                            </v-card-subtitle>
                            <v-card-subtitle class="py-1 subtitle-1">Category: {{viewCategory}}</v-card-subtitle>
                            <v-card-subtitle class="py-1 subtitle-1">Location: {{viewLocation}}</v-card-subtitle>
                            <v-card-subtitle class="py-1 subtitle-1">Date: {{viewDate}}</v-card-subtitle>                            
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

                    <v-row
                        class="mb-5"
                    >
                        <v-col
                            col="12"
                            md="12"
                            sm="12"
                            xs="12"
                            style="border-bottom: 1px solid #eaeaea"
                            class="text-h5 d-flex align-center flex-wrap"
                        >
                            <span>Author</span>

                            <v-spacer></v-spacer>

                            <div>
                                <NuxtLink to="/Dashboard/Blogs/Author-Detail">
                                    <v-btn
                                        class="ml-3"
                                        color="primary"
                                    >
                                        Edit Author
                                    </v-btn>
                                </NuxtLink>
                            </div>
                        </v-col>
                        <v-col
                            col="12"
                            xs="12"
                        >
                            <v-row
                                class="d-flex align-center flex-wrap"
                            >
                                <v-col
                                    col="12"
                                    md="3"
                                    sm="4"
                                    xs="12"
                                >
                                    <v-img
                                        :src="viewAuthorProfilePicture"
                                    ></v-img>
                                </v-col>
                                <v-col
                                    col="12"
                                    md="9"
                                    sm="8"
                                    xs="12"
                                >
                                    <div class="text-h5 pl-4 pt-0">{{viewAuthorName}}</div>
                                    <div class="pt-1 pl-4 pb-3 subtitle-1">
                                        {{viewAuthorDescription}}
                                    </div>
                                    <div class="text-p pl-4 black--text">
                                        <div class="pb-2">
                                            Facebook: {{viewAuthorFacebookLink}}
                                        </div>
                                        <div class="pb-2">
                                            Twitter: {{viewAuthorTwitterLink}}
                                        </div>
                                        <div class="pb-2">
                                            Instagram: {{viewAuthorInstagramLink}}
                                        </div>
                                        <div class="pb-2">
                                            Youtube: {{viewAuthorYoutubeLink}}
                                        </div>
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
                        label="Blog Id"
                        outlined
                        required
                        readonly
                    ></v-text-field>

                    <v-text-field
                        v-model="title"
                        :rules="inputRules"
                        label="Blog Title"
                        outlined
                        required
                    ></v-text-field>

                    <v-select
                        v-model="category"
                        :items="categories"
                        item-value="catId"
                        item-text="cat"
                        :rules="inputRules"
                        label="Category"
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
                        v-model="bannerImage"
                        label="Blog Image"
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

                    <v-menu
                        ref="menu"
                        v-model="menu"
                        :close-on-content-click="false"
                        :return-value.sync="date"
                        transition="scale-transition"
                        offset-y
                        min-width="auto"
                    >
                        <template v-slot:activator="{ on, attrs }">
                            <v-text-field
                                v-model="date"
                                label="Date"
                                prepend-inner-icon="mdi-calendar"
                                readonly
                                v-bind="attrs"
                                v-on="on"
                                outlined
                            ></v-text-field>
                        </template>
                        <v-date-picker
                            v-model="date"
                            no-title
                            scrollable
                        >
                            <v-spacer></v-spacer>
                            <v-btn
                                text
                                color="primary"
                                @click="menu = false"
                            >
                                Cancel
                            </v-btn>
                            <v-btn
                                text
                                color="primary"
                                @click="$refs.menu.save(date)"
                            >
                                OK
                            </v-btn>
                        </v-date-picker>
                    </v-menu>

                    <client-only>
                        <vue-editor 
                            placeholder="Speaker Description... " 
                            v-model="description" 
                            required
                            class="mb-9"
                        ></vue-editor>
                    </client-only>

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

                    <v-select
                        v-model="author"
                        :items="authors"
                        item-value="id"
                        item-text="name"
                        :rules="inputRules"
                        label="Author"
                        outlined
                        required
                    ></v-select>

                    <v-btn
                        :disabled="!valid"
                        class="btn-style mr-4"
                        large
                        @click="UpdateBlogInfo"
                        elevation="0"
                    >
                        Update Blog Info
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
            blog:[
                {
                    id: '1',
                    title: 'Top 20 Event and Conference Country',
                    catId: 3,
                    category: 'lists',
                    locId: 2,
                    location: 'Paris', 
                    shortDescription: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has. Sed ad dicam platonem, mea eros illum elitr id, ei has similique constituto.',
                    description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has. Sed ad dicam platonem, mea eros illum elitr id, ei has similique constituto. Ea movet saperet rationibus sit, pri autem aliquip invidunt an. Consetetur omittantur consequuntur eos et. <strong> Eleifend praesent iudicabit no mea, tollit persequeris ex pri, tota splendide voluptaria in pri.</strong> Ad per tale aliquip, ei sit viris commune albucius. Eos aliquip scaevola ut, eum alii mentitum prodesset no, his ne suas atomorum. Et numquam deleniti ponderum vis, quod error at mei. Novum blandit adolescens sea te. Ea eum cetero scaevola.<br /><br />In his meis porro viris, illud imperdiet reprimique et vim. Feugiat atomorum reprehendunt vix ei, ei facete regione pri. Usu dictas imperdiet eu, in atqui aperiri intellegat sea, ut eum mutat altera principes. Te sit quaeque oportere, has modus inani ceteros ad. Impedit blandit deseruisse duo ea, ne graecis deleniti incorrupte usu. Ut mei splendide accommodare. An pri iisque meliore, eam ei splendide eloquentiam philosophia. <u>Ne per meis eleifend electram.</u> Ne eam porro aliquam invidunt. Minim docendi eloquentiam cum ad. Quo ea mazim ubique, ex est fuisset blandit scaevola. Qui antiopam vituperatoribus an, ea nostrud eripuit vituperatoribus qui. In eam diam nominati, per ea alia luptatum. <span class="yellowish--text">Nam habemus electram democritum ut.</span> Mei ea omnium admodum intellegat. Habeo atqui molestiae at mei, an nec ridens consequuntur. Quem nulla cum ei, his ipsum apeirian no, per at eius iriure aperiri. Sed dicam interesset ei. Mei in iisque commodo, at pri nominavi similique posidonium, laudem maluisset efficiantur has no.<br/><br /><br />His verterem consectetuer consequuntur ne, no virtute atomorum usu. <b> Eu quo nemore causae tacimates, eos viderer persequeris an.</b> Cu molestie consulatu qui. Natum labores perfecto no ius, pri dico mundi inciderint id. Ei usu dico libris postea. Cu graeco doctus splendide qui, ei eum probo regione.', 
                    date: 'November 23, 2018',
                    url: require('../assets/Images/Blog/blog1.png'), 
                    status: 'Pending',
                    statusId: 2, 
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
                    ],
                    authorId: 3,
                    authorName: 'Author 3', 
                    authorDescription: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has.',
                    authorFacebookLink: 'www.facebook.com',
                    authorTwitterLink: 'www.twitter.com',
                    authorInstagramLink: 'www.instagram.com',
                    authorYoutubeLink: 'www.youtube.com',
                    authorProfilePicture: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/avatar-150x150.jpg', 
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

            viewTitle: '',
            viewCategory: '',
            viewLocation: '',
            viewDescription: '',
            viewShortDescription: '',
            viewBannerImage: null,
            viewDate: '' ,
            viewTags:[],
            viewAuthorName: '',
            viewAuthorDescription: '',
            viewAuthorFacebookLink:'',
            viewAuthorTwitterLink:'',
            viewAuthorInstagramLink:'',
            viewAuthorYoutubeLink:'',
            viewAuthorProfilePicture: null,

            id: '',
            title: '',
            category: {},
            location: {},
            description: '',
            shortDescription: '',
            bannerImage: null,
            // date: '', 
            tags:[],
            author: [], 
            authorName: '', 
            authorDescription: '',
            authorFacebookLink: '',
            authorTwitterLink: '',
            authorInstagramLink: '',
            authorYoutubeLink: '',
            authorProfilePicture: '', 

            date: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10),
            menu: false,

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
            statusId: '', 
            snackbar: false,
            snackbarText: '' ,
            valid: true,
            
            inputRules: [
                v => !!v || 'This Field is Required',
            ],
            

        }),
        methods: {
            async UpdateBlogInfo(){
                if(this.$refs.form.validate()){
                    this.snackbarText= 'Speaker Info Updated Successfully';
                    this.snackbar= true; 
                    this.viewMode= true; 
                }
            },
            async reset(){
                this.$nuxt.$router.push({path: '/Dashboard/Blogs/All-Blogs'})
            },
            async approveBlog(){
                this.snackbarText= 'Blog Approved Successfully';
                this.snackbar= true; 
                this.statusID = '1' ; 
                this.viewMode= true; 
            }
        },
        mounted() { 
            this.id = this.blog[0].id; 

            this.viewTitle = this.blog[0].title;
            this.viewCategory = this.blog[0].category;
            this.viewLocation = this.blog[0].location;
            this.viewDescription = this.blog[0].description;
            this.viewShortDescription = this.blog[0].shortDescription;
            this.viewBannerImage =  this.blog[0].url;
            this.viewDate = this.blog[0].date;
            this.viewTags = this.blog[0].tags;

            this.viewAuthorName= this.blog[0].authorName;
            this.viewAuthorDescription= this.blog[0].authorDescription;
            this.shortDescription = this.blog[0].shortDescription;
            this.viewAuthorFacebookLink= this.blog[0].authorFacebookLink;
            this.viewAuthorTwitterLink= this.blog[0].authorTwitterLink;
            this.viewAuthorInstagramLink= this.blog[0].AuthorInstagramLink;
            this.viewAuthorYoutubeLink= this.blog[0].authorYoutubeLink;
            this.viewAuthorProfilePicture= this.blog[0].authorProfilePicture;

            this.title = this.blog[0].title;
            this.category = { id: this.blog[0].catId, cat: this.blog[0].category };
            this.location = { id: this.blog[0].locId, location: this.blog[0].location };
            this.author = { id: this.blog[0].authorId, author: this.blog[0].authorName };
            this.description = this.blog[0].description;
            this.bannerImage =  this.blog[0].url;
            // this.date =  this.blog[0].date;
            this.tags = this.blog[0].tags;
            this.authorName= this.blog[0].authorName;
            this.authorDescription= this.blog[0].authorDescription;
            this.authorFacebookLink= this.blog[0].authorFacebookLink;
            this.authorTwitterLink= this.blog[0].authorTwitterLink;
            this.authorInstagramLink= this.blog[0].AuthorInstagramLink;
            this.authorYoutubeLink= this.blog[0].authorYoutubeLink;
            // this.authorProfilePicture= this.blog.authorProfilePicture;
            // console.log(tags);
            this.statusId = this.blog[0].statusId;
        }
    }
</script>