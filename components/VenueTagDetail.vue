<template>
    <div>
        <div
            class="title-text mb-5"
        >
            Venue Tag Detail
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
                                <v-list-item-subtitle class="subtitle-1 mt-2">{{viewTagId}}</v-list-item-subtitle>
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
                                <v-list-item-title class="text-h6 font-weight-regular">Tag</v-list-item-title>
                                <v-list-item-subtitle class="subtitle-1 mt-2">{{viewTag}}</v-list-item-subtitle>
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
                        label="Tag Id"
                        outlined
                        required
                        readonly
                    ></v-text-field>

                    <v-text-field
                        v-model="tag"
                        :rules="inputRules"
                        label="Tag"
                        outlined
                        required
                    ></v-text-field>

                    <v-btn
                        :disabled="!valid"
                        class="btn-style mr-4"
                        large
                        @click="UpdateTagInfo"
                        elevation="0"
                    >
                        Update Tag Info
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
        name: 'VenueTagDetail',
        data:()=>({
            viewMode: true,
            tagSelected:[
                {
                    id: 4,
                    tag: 'Food',
                }
            ],
            
            snackbar: false,
            snackbarText: '' ,
            valid: true,
            id: '',
            category: '',
            inputRules: [
                v => !!v || 'Tag is required',
            ],
            viewTagId: '',
            viewTag: '',
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

        }),
        methods: {
            async UpdateTagInfo(){
                if(this.$refs.form.validate()){
                    let checkTag = this.tags.find(x=> x.tag == this.tag);
                    if(checkTag){
                        this.snackbarText= 'Tag Already Exist';
                        this.snackbar= true; 
                    }
                    else{
                        this.snackbarText= 'Tag Info Updated Successfully';
                        this.snackbar= true;  
                    }
                }
            },
            async reset(){
                this.$nuxt.$router.push({path: '/Dashboard/Venues/All-Tags'})
            }
        },
        mounted() {
            this.id = this.tagSelected[0].id; 
            this.tag = this.tagSelected[0].tag;
            this.viewTagId = this.tagSelected[0].id; 
            this.viewTag = this.tagSelected[0].tag;
        }
    }
</script>