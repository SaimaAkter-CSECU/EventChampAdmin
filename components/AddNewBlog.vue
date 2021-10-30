<template>
    <div>
        <div
            class="title-text mb-5"
        >
            Add New Blog
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
                        label="Blog Title"
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

                    <client-only>
                        <vue-editor 
                            placeholder="Description..." 
                            v-model="description" 
                            required
                            class="mb-5"
                        ></vue-editor>
                    </client-only>

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

                    <v-file-input
                        v-model="blogImage"
                        label="Blog Image"
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

                    <v-btn
                        :disabled="!valid"
                        class="btn-style mr-4"
                        large
                        @click="addBlog"
                        elevation="0"
                    >
                        Add Blog
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
        name: 'AddNewBlog',
        data: ()=>({
            valid: true,
            date: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10),
            menu: false,

            title: '',
            category: null,
            description: '', 
            tag: null,
            blogImage: null, 
            inputRules: [
                v => !!v || 'Name is required',
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
            async addBlog() {
                if(this.$refs.form.validate()){
                    this.snackbarText= 'Blog Added Successfully';
                    this.snackbar= true; 
                    this.$refs.form.reset(); 
                }
            },
            async reset () {
                this.$refs.form.reset();
                this.$nuxt.$router.push({path:'/Dashboard/Blogs/All-Blogs'})

            },
        },
    }
</script>