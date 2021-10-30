<template>
    <div>
        <div
            class="title-text mb-5"
        >
            Venue Location Detail
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
                <v-row>
                    <v-col
                        col="12"
                        md="4"
                        sm="6"
                        xs="12"
                    >
                        <v-list-item two-line>
                            <v-list-item-content>
                                <v-list-item-title class="text-h6 font-weight-regular">id</v-list-item-title>
                                <v-list-item-subtitle class="subtitle-1 mt-2">{{viewLocationId}}</v-list-item-subtitle>
                            </v-list-item-content>
                        </v-list-item>
                    </v-col>
                    <v-col
                        col="12"
                        md="4"
                        sm="6"
                        xs="12"
                    >
                        <v-list-item two-line>
                            <v-list-item-content>
                                <v-list-item-title class="text-h6 font-weight-regular">Location</v-list-item-title>
                                <v-list-item-subtitle class="subtitle-1 mt-2">{{viewLocation}}</v-list-item-subtitle>
                            </v-list-item-content>
                        </v-list-item>
                    </v-col>
                </v-row>
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
                        label="Location Id"
                        outlined
                        required
                        readonly
                    ></v-text-field>

                    <v-text-field
                        v-model="location"
                        :rules="inputRules"
                        label="Location"
                        outlined
                        required
                    ></v-text-field>

                    <v-btn
                        :disabled="!valid"
                        class="btn-style mr-4"
                        large
                        @click="UpdateLocationInfo"
                        elevation="0"
                    >
                        Update Location Info
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
        name: 'VenueLocationDetail',
        data:()=>({
            viewMode: true,
            loc:[
                {
                    id: 2,
                    location: 'Paris',
                }
            ],
            
            snackbar: false,
            snackbarText: '' ,
            valid: true,
            id: '',
            location: '',
            inputRules: [
                v => !!v || 'Location is required',
            ],
            viewLocationId: '',
            viewLocation: '',
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

        }),
        methods: {
            async UpdateLocationInfo(){
                if(this.$refs.form.validate()){
                    let checkLocation = this.locations.find(x=> x.location == this.location);
                    if(checkLocation){
                        this.snackbarText= 'Location Already Exist';
                        this.snackbar= true; 
                    }
                    else{
                        this.snackbarText= 'Location Info Updated Successfully';
                        this.snackbar= true;  
                    }
                }
            },
            async reset(){
                this.$nuxt.$router.push({path: '/Dashboard/Venues/All-Locations'})
            }
        },
        mounted() {
            this.id = this.loc[0].id; 
            this.location = this.loc[0].location;
            this.viewLocationId = this.loc[0].id; 
            this.viewLocation = this.loc[0].location;
        }
    }
</script>