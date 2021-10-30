<template>
    <div>
        <div
            class="title-text mb-5"
        >
            Add New Speaker
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

                    <v-select
                        v-model="category"
                        :items="categories"
                        item-text="cat"
                        item-value="id"
                        :rules="[v => !!v || 'Category is required']"
                        label="User Category/ Designation"
                        outlined
                        required
                    ></v-select>

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
                        label="Speaker Image Gallery"
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
                        @click="addSpeaker"
                        elevation="0"
                    >
                        Add Speaker
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
        name: 'AddNewSpeaker',
        data: ()=>({
            valid: true,
            name: '',
            category: null,
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
            async addSpeaker() {
                if(this.$refs.form.validate()){
                    this.snackbarText= 'Speaker Added Successfully';
                    this.snackbar= true; 
                    this.$refs.form.reset(); 
                }
            },
            async reset () {
                this.$refs.form.reset();
                this.$nuxt.$router.push({path:'/Dashboard/Speakers/All-Speakers'})

            },
        },
    }
</script>