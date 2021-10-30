<template>
    <div>
        <div
            class="title-text mb-5"
        >
            Speaker Category Detail
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
                                <v-list-item-subtitle class="subtitle-1 mt-2">{{viewCategoryId}}</v-list-item-subtitle>
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
                                <v-list-item-title class="text-h6 font-weight-regular">Category</v-list-item-title>
                                <v-list-item-subtitle class="subtitle-1 mt-2">{{viewCategory}}</v-list-item-subtitle>
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
                        label="Catehory Id"
                        outlined
                        required
                        readonly
                    ></v-text-field>

                    <v-text-field
                        v-model="category"
                        :rules="inputRules"
                        label="Category"
                        outlined
                        required
                    ></v-text-field>

                    <v-btn
                        :disabled="!valid"
                        class="btn-style mr-4"
                        large
                        @click="UpdateCategoryInfo"
                        elevation="0"
                    >
                        Update Category Info
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
        name: 'SpeakerCategoryDetail',
        data:()=>({
            viewMode: true,
            cat:[
                {
                    id: 2,
                    category: 'Model',
                }
            ],
            
            snackbar: false,
            snackbarText: '' ,
            valid: true,
            id: '',
            category: '',
            inputRules: [
                v => !!v || 'Category is required',
            ],
            viewCategoryId: '',
            viewCategory: '',
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

        }),
        methods: {
            async UpdateCategoryInfo(){
                if(this.$refs.form.validate()){
                    let checkCategory = this.categories.find(x=> x.category == this.category);
                    if(checkCategory){
                        this.snackbarText= 'Category Already Exist';
                        this.snackbar= true; 
                    }
                    else{
                        this.snackbarText= 'Category Info Updated Successfully';
                        this.snackbar= true;  
                    }
                }
            },
            async reset(){
                this.$nuxt.$router.push({path: '/Dashboard/Speakers/All-Categories'})
            }
        },
        mounted() {
            this.id = this.cat[0].id; 
            this.category = this.cat[0].category;
            this.viewCategoryId = this.cat[0].id; 
            this.viewCategory = this.cat[0].category;
        }
    }
</script>