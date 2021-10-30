<template>
    <div>
        <div
            class="title-text mb-5"
        >
            Venue Detail
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
                            md="12"
                            sm="12"
                            xs="12"
                        >
                            <v-card-title class="text-h5 pt-0 font-weight-medium">{{viewTitle}}</v-card-title>
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
                                <div class="pb-2">
                                    Working Hours (Weekdays): {{viewWorkingHoursWeekdays}}
                                </div>
                                <div class="pb-2">
                                    Working Hours (Saturday): {{viewWorkingHoursSaturday}}
                                </div>
                                <div class="pb-2">
                                    Working Hours (Sunday): {{viewWorkingHoursSunday}}
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
                            class="text-h5 mb-5"
                        >
                            Sponsors
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
                                    v-for="viewSponsor in viewSponsors"
                                    :key="viewSponsor.id"
                                >
                                    <v-img
                                        :src="viewSponsor.img"
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
                        label="Venue Id"
                        outlined
                        required
                        readonly
                    ></v-text-field>

                    <v-text-field
                        v-model="title"
                        :rules="inputRules"
                        label="Venue Title"
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
                        label="Phone"
                        outlined
                        required
                    ></v-text-field>

                    <v-text-field
                        v-model="email"
                        :rules="inputRules"
                        label="Email"
                        outlined
                        required
                    ></v-text-field>

                    <v-menu
                        ref="menu"
                        v-model="menu"
                        :close-on-content-click="false"
                        :return-value.sync="start"
                        transition="scale-transition"
                        offset-y
                        min-width="auto"
                    >
                        <template v-slot:activator="{ on, attrs }">
                            <v-text-field
                                v-model="start"
                                label="Weekdays Openning Time"
                                prepend-inner-icon="mdi-timer-sand"
                                readonly
                                v-bind="attrs"
                                v-on="on"
                                outlined
                            ></v-text-field>
                        </template>
                        <v-time-picker
                            v-model="start"
                            :max="end"
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
                                @click="$refs.menu.save(start)"
                            >
                                OK
                            </v-btn>
                        </v-time-picker>
                    </v-menu>
                    <v-menu
                        ref="menu2"
                        v-model="menu2" 
                        :close-on-content-click="false"
                        :return-value.sync="end"
                        transition="scale-transition"
                        offset-y
                        min-width="auto"
                    >
                        <template v-slot:activator="{ on, attrs }">
                            <v-text-field
                                v-model="end"
                                label="Weekdays Closing Time"
                                prepend-inner-icon="mdi-timer-sand"
                                readonly
                                v-bind="attrs"
                                v-on="on"
                                outlined
                            ></v-text-field>
                        </template>
                        <v-time-picker
                            v-model="end"
                            :min="start"
                            scrollable
                        >
                            <v-spacer></v-spacer>
                            <v-btn
                                text
                                color="primary"
                                @click="menu2 = false"
                            >
                                Cancel
                            </v-btn>
                            <v-btn
                                text
                                color="primary"
                                @click="$refs.menu2.save(end)"
                            >
                                OK
                            </v-btn>
                        </v-time-picker>
                    </v-menu>

                    <v-menu
                        ref="menu3"
                        v-model="menu3"
                        :close-on-content-click="false"
                        :return-value.sync="saturdayStart"
                        transition="scale-transition"
                        offset-y
                        min-width="auto"
                    >
                        <template v-slot:activator="{ on, attrs }">
                            <v-text-field
                                v-model="saturdayStart"
                                label="Saturday Openning Time"
                                prepend-inner-icon="mdi-timer-sand"
                                readonly
                                v-bind="attrs"
                                v-on="on"
                                outlined
                            ></v-text-field>
                        </template>
                        <v-time-picker
                            v-model="saturdayStart"
                            :max="saturdayEnd"
                            scrollable
                        >
                            <v-spacer></v-spacer>
                            <v-btn
                                text
                                color="primary"
                                @click="menu3 = false"
                            >
                                Cancel
                            </v-btn>
                            <v-btn
                                text
                                color="primary"
                                @click="$refs.menu3.save(saturdayStart)"
                            >
                                OK
                            </v-btn>
                        </v-time-picker>
                    </v-menu>
                    <v-menu
                        ref="menu4"
                        v-model="menu4" 
                        :close-on-content-click="false"
                        :return-value.sync="saturdayEnd"
                        transition="scale-transition"
                        offset-y
                        min-width="auto"
                    >
                        <template v-slot:activator="{ on, attrs }">
                            <v-text-field
                                v-model="saturdayEnd"
                                label="Saturday Closing Time"
                                prepend-inner-icon="mdi-timer-sand"
                                readonly
                                v-bind="attrs"
                                v-on="on"
                                outlined
                            ></v-text-field>
                        </template>
                        <v-time-picker
                            v-model="saturdayEnd"
                            :min="saturdayStart"
                            scrollable
                        >
                            <v-spacer></v-spacer>
                            <v-btn
                                text
                                color="primary"
                                @click="menu4 = false"
                            >
                                Cancel
                            </v-btn>
                            <v-btn
                                text
                                color="primary"
                                @click="$refs.menu4.save(saturdayEnd)"
                            >
                                OK
                            </v-btn>
                        </v-time-picker>
                    </v-menu>

                    <v-menu
                        ref="menu5"
                        v-model="menu5"
                        :close-on-content-click="false"
                        :return-value.sync="sundayStart"
                        transition="scale-transition"
                        offset-y
                        min-width="auto"
                    >
                        <template v-slot:activator="{ on, attrs }">
                            <v-text-field
                                v-model="sundayStart"
                                label="Sunday Openning Time"
                                prepend-inner-icon="mdi-timer-sand"
                                readonly
                                v-bind="attrs"
                                v-on="on"
                                outlined
                            ></v-text-field>
                        </template>
                        <v-time-picker
                            v-model="sundayStart"
                            :max="sundayEnd"
                            scrollable
                        >
                            <v-spacer></v-spacer>
                            <v-btn
                                text
                                color="primary"
                                @click="menu5 = false"
                            >
                                Cancel
                            </v-btn>
                            <v-btn
                                text
                                color="primary"
                                @click="$refs.menu5.save(sundayStart)"
                            >
                                OK
                            </v-btn>
                        </v-time-picker>
                    </v-menu>
                    <v-menu
                        ref="menu6"
                        v-model="menu6" 
                        :close-on-content-click="false"
                        :return-value.sync="sundayEnd"
                        transition="scale-transition"
                        offset-y
                        min-width="auto"
                    >
                        <template v-slot:activator="{ on, attrs }">
                            <v-text-field
                                v-model="sundayEnd"
                                label="Sunday Closing Time"
                                prepend-inner-icon="mdi-timer-sand"
                                readonly
                                v-bind="attrs"
                                v-on="on"
                                outlined
                            ></v-text-field>
                        </template>
                        <v-time-picker
                            v-model="sundayEnd"
                            :min="sundayStart"
                            scrollable
                        >
                            <v-spacer></v-spacer>
                            <v-btn
                                text
                                color="primary"
                                @click="menu6 = false"
                            >
                                Cancel
                            </v-btn>
                            <v-btn
                                text
                                color="primary"
                                @click="$refs.menu6.save(sundayEnd)"
                            >
                                OK
                            </v-btn>
                        </v-time-picker>
                    </v-menu>

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

                    <v-file-input 
                        v-model="bannerImage"
                        label="Venue Image"
                        prepend-icon=""
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

                    <v-text-field
                        v-model="noOfSponsors"
                        type="number"
                        label="No of Sponsors"
                        @change="populateSponsorField()"
                        outlined
                    ></v-text-field>

                    <div v-show="fieldNo > 0">
                        <div
                            v-for="i in `${fieldNo}`"
                            :key="i"
                        >
                            <v-text-field
                                :v-model="`sponsorLink${i}`"
                                label="Sponsor Link"
                                required
                                outlined
                            >
                            </v-text-field>
                             <!-- <v-text-field
                                :value="`sponsorImage${i}`"
                                label="Sponsor Image Link"
                                prepend-icon=""
                                outlined
                            >
                            </v-text-field> -->
                            <v-file-input 
                                :v-model="`sponsorImage${i}`"
                                label="Venue Sponsor Image"
                                prepend-icon=""
                                outlined
                            >
                            </v-file-input>
                        </div>
                    </div>


                    <v-btn
                        :disabled="!valid"
                        class="btn-style mr-4"
                        large
                        @click="UpdateVenueInfo"
                        elevation="0"
                    >
                        Update Venue Info
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
        name: 'VenueDetail', 
        data:()=>({
            viewMode: true,
            venues:[
                {
                    id: 1, 
                    title: 'Oxnard Beach',
                    shortDescription: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has. Sed ad dicam platonem, mea eros illum elitr id, ei has similique constituto. ',
                    description: 'Lorem ipsum dolor sit amet, voluptua iracundia disputationi an pri, his utinam principes dignissim ad. Ne nec dolore oblique nusquam, cu luptatum volutpat delicatissimi has. Sed ad dicam platonem, mea eros illum elitr id, ei has similique constituto. Ea movet saperet rationibus sit, pri autem aliquip invidunt an. Consetetur omittantur consequuntur eos et. <strong> Eleifend praesent iudicabit no mea, tollit persequeris ex pri, tota splendide voluptaria in pri.</strong> Ad per tale aliquip, ei sit viris commune albucius. Eos aliquip scaevola ut, eum alii mentitum prodesset no, his ne suas atomorum. Et numquam deleniti ponderum vis, quod error at mei. Novum blandit adolescens sea te. Ea eum cetero scaevola.<br /><br />In his meis porro viris, illud imperdiet reprimique et vim. Feugiat atomorum reprehendunt vix ei, ei facete regione pri. Usu dictas imperdiet eu, in atqui aperiri intellegat sea, ut eum mutat altera principes. Te sit quaeque oportere, has modus inani ceteros ad. Impedit blandit deseruisse duo ea, ne graecis deleniti incorrupte usu. Ut mei splendide accommodare. An pri iisque meliore, eam ei splendide eloquentiam philosophia. <u>Ne per meis eleifend electram.</u> Ne eam porro aliquam invidunt. Minim docendi eloquentiam cum ad. Quo ea mazim ubique, ex est fuisset blandit scaevola. Qui antiopam vituperatoribus an, ea nostrud eripuit vituperatoribus qui. In eam diam nominati, per ea alia luptatum. <span class="yellowish--text">Nam habemus electram democritum ut.</span> Mei ea omnium admodum intellegat. Habeo atqui molestiae at mei, an nec ridens consequuntur. Quem nulla cum ei, his ipsum apeirian no, per at eius iriure aperiri. Sed dicam interesset ei. Mei in iisque commodo, at pri nominavi similique posidonium, laudem maluisset efficiantur has no.<br/><br /><br />His verterem consectetuer consequuntur ne, no virtute atomorum usu. <b> Eu quo nemore causae tacimates, eos viderer persequeris an.</b> Cu molestie consulatu qui. Natum labores perfecto no ius, pri dico mundi inciderint id. Ei usu dico libris postea. Cu graeco doctus splendide qui, ei eum probo regione.', 
                    weekdays: '09:00 - 22:30', 
                    saturday: '09:00 - 23:59', 
                    sunday: 'Closed', 

                    location: 'Callifornia', 
                    address: 'Harbiye Mahallesi, Darülbedai Caddesi No:3, 34367 Şişli/İstanbul',
                    catId: 9,
                    category: 'Beach', 
                    
                    phone: '0674 987 665',
                    email: 'event@gloriathemes.com', 
                    website: 'www.website.com',
                    
                    url: require('../assets/Images/LatestPost/LatestPost1.png'),

                    facebookLink: 'http://www.facebook.com',
                    instagramLink: 'http://www.instagram.com', 
                    youtubeLink: 'http://www.youtube.com', 
                    twitterLink: 'http://www.facebook.com', 
                    whishCount: 7, 
                    
                    photos: [
                        {
                            id: 1, 
                            url : 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/event-3-350x350.jpg',
                        },
                        {
                            id: 2, 
                            url : 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/event-3-350x350.jpg',
                        },
                        {
                            id: 3, 
                            url : 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/event-3-350x350.jpg',
                        },
                        {
                            id: 4, 
                            url : 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/event-3-350x350.jpg',
                        },
                        {
                            id: 5, 
                            url : 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/event-3-350x350.jpg',
                        },
                        {
                            id: 6, 
                            url : 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/event-3-350x350.jpg',
                        },
                        {
                            id: 7, 
                            url : 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/event-3-350x350.jpg',
                        },
                        {
                            id: 8, 
                            url : 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/event-3-350x350.jpg',
                        },
                        {
                            id: 9, 
                            url : 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/event-3-350x350.jpg',
                        }
                    ],
                    sponsors: [
                        {
                            id: 1,
                            link: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                            img: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                        },
                        {
                            id: 2,
                            link: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                            img: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                        },
                        {
                            id: 3,
                            link: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                            img: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                        },
                        {
                            id: 4,
                            link: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                            img: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                        },
                        {
                            id: 5,
                            link: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                            img: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                        },
                        {
                            id: 6,
                            link: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                            img: 'https://demo.gloriathemes.com/eventchamp/demo/wp-content/uploads/2018/11/sponsor-1-250x220.jpg',
                        },
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

            viewTitle: '',
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
            viewWorkingHoursWeekdays: '',
            viewWorkingHoursSaturday: '',
            viewWorkingHoursSunday: '',
            viewBannerImage: '',
            viewSponsors: [], 
            viewPhotos: [], 
            viewTags: [], 

            id: '',
            title: '',
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
            bannerImage: null,
            workingHoursWeekdays: '',
            workingHoursSaturday: '',
            workingHoursSunday: '', 
            menu: false,
            menu2: false, 
            menu3: false,
            menu4: false,
            menu5: false,
            menu6: false,
            start: null,
            end: null,
            saturdayStart: null,
            saturdayEnd: null,
            sundayStart: null,
            sundayEnd: null,
            photos: [],
            tags: [],
            noOfSponsors: '', 
            fieldNo: 0, 

            url: null, 
            
            snackbar: false,
            snackbarText: '' ,
            valid: true,
            
            inputRules: [
                v => !!v || 'This Field is Required',
            ],
            

        }),
        methods: {
            async UpdateVenueInfo(){
                if(this.$refs.form.validate()){
                    this.snackbarText= 'Venue Info Updated Successfully';
                    this.snackbar= true; 
                    this.viewMode= true; 
                }
            },
            async reset(){
                this.$nuxt.$router.push({path: '/Dashboard/Venues/All-Venues'})
            },
            async populateSponsorField(){
                // console.log(this.noOfSponsors); 
                this.fieldNo = this.noOfSponsors;
                console.log(this.fieldNo)
            }
        },
        mounted() {
            this.id = this.venues[0].id; 

            this.viewTitle = this.venues[0].title;
            this.viewCategory = this.venues[0].category;
            this.viewLocation = this.venues[0].location;
            this.viewAddress = this.venues[0].address;
            this.viewShortDescription = this.venues[0].shortDescription;
            this.viewWorkingHoursWeekdays = this.venues[0].weekdays;
            this.viewWorkingHoursSaturday = this.venues[0].saturday;
            this.viewWorkingHoursSunday = this.venues[0].sunday;
            this.viewPhone = this.venues[0].phone;
            this.viewEmail = this.venues[0].email;
            this.viewWebsiteLink = this.venues[0].website;
            this.viewFacebookLink = this.venues[0].facebookLink;
            this.viewTwitterLink = this.venues[0].twitterLink;
            this.viewInstagramLink = this.venues[0].instagramLink;
            this.viewYoutubeLink = this.venues[0].youtubeLink;
            this.viewDescription = this.venues[0].description;
            this.viewBannerImage =  this.venues[0].url;
            this.viewPhotos = this.venues[0].photos;
            this.viewTags = this.venues[0].tags;
            this.viewSponsors = this.venues[0].sponsors; 

            this.title = this.venues[0].title;
            this.category = { id: this.venues[0].catId, cat: this.venues[0].category };
            this.location = { id: this.venues[0].locId, location: this.venues[0].location };
            // this.location = this.speaker[0].location;
            this.address = this.venues[0].address;
            this.shortDescription = this.venues[0].shortDescription;
            this.phone = this.venues[0].phone;
            this.email = this.venues[0].email;
            this.websiteLink = this.venues[0].website;
            this.facebookLink = this.venues[0].facebookLink;
            this.twitterLink = this.venues[0].twitterLink;
            this.instagramLink = this.venues[0].instagramLink;
            this.youtubeLink = this.venues[0].youtubeLink;
            this.description = this.venues[0].description;
            this.shortDescription = this.venues[0].shortDescription;
            this.bannerImage =  this.venues[0].url;
            // this.profilePicture = this.speaker[0].profilePicture;
            // this.photos = this.speaker[0].photos;
            this.tags = this.venues[0].tags;
            this.sponsors = this.venues[0].sponsors;
        }
    }
</script>