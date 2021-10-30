<template>
    <div>
        <div
            class="title-text mb-5"
        >
            Add New Venue
        </div>
        <div>   
            <v-card class="pa-7">
                <v-form
                    ref="form"
                    v-model="valid"
                    lazy-validation
                >
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
                        item-text="cat"
                        item-value="id"
                        :rules="[v => !!v || 'Category is required']"
                        label="Category"
                        outlined
                        required
                    ></v-select>

                    <v-textarea
                        v-model="shortDescription"
                        :rules="inputRules"
                        label="Short Description"
                        rows="3"
                        outlined
                        required
                    ></v-textarea>

                    <client-only>
                        <vue-editor 
                            placeholder="Description..." 
                            v-model="description" 
                            required
                            class="mb-5"
                        ></vue-editor>
                    </client-only>

                    <v-select
                        v-model="location"
                        :items="locations"
                        item-text="location"
                        item-value="id"
                        :rules="[v => !!v || 'Location is required']"
                        label="User Location"
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
                        v-model="email"
                        :rules="emailRules"
                        label="email"
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
                        v-model="webLink"
                        label="Website Link"
                        outlined
                    ></v-text-field>

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
                        label="Speaker Image"
                        prepend-icon=""
                        prepend-inner-icon="mdi-camera"
                        outlined
                        required
                    ></v-file-input>

                    <v-select
                        v-model="tag"
                        :items="tags"
                        item-text="tag"
                        item-value="id"
                        :rules="[v => !!v || 'Tags are required']"
                        chips
                        label="Tags"
                        multiple
                        outlined
                        required
                    ></v-select>

                    <v-file-input
                        label="Venue Image Gallery"
                        prepend-icon=""
                        prepend-inner-icon="mdi-camera"
                        outlined
                        chips
                        multiple 
                        required
                    ></v-file-input>

                    <v-btn
                        :disabled="!valid"
                        class="btn-style mr-4"
                        large
                        @click="addVenue"
                        elevation="0"
                    >
                        Add Venue
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
        name: 'AddNewVenue',
        data: ()=>({
            valid: true,
            // date: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10),
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

            title: '',
            name: '',
            category: null,
            shortDescription: '', 
            description: '', 
            location: null,
            address: '', 
            email: '',
            phone: '',
            webLink: '',
            fbLink: '',
            twitterLink: '',
            youtubeLink: '',
            instaLink: '',
            tag: null,
            inputRules: [
                v => !!v || 'Name is required',
            ],
            emailRules: [
                v => !!v || 'E-mail is required',
                v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
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
            ],
            tags:[
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
            
            snackbar: false,
            snackbarText: '' , 
        }),
        methods: {
            async addVenue() {
                if(this.$refs.form.validate()){
                    this.snackbarText= 'Venue Added Successfully';
                    this.description= ''; 
                    this.snackbar= true; 
                    this.$refs.form.reset(); 
                }
            },
            async reset () {
                this.$refs.form.reset();
                this.$nuxt.$router.push({path:'/Dashboard/Venues/All-Venues'})

            },
        },
    }
</script>