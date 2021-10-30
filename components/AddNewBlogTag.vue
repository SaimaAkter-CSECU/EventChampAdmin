<template>
    <div>
        <div
            class="title-text mb-5"
        >
            Add New Tag
        </div>
        <div>           
            <v-form
                ref="form"
                v-model="valid"
                lazy-validation
            >
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
                    @click="addTag"
                    elevation="0"
                >
                    Add Tag
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
        name: 'AddNewBlogTag',
        data: ()=>({
            valid: true,
            tag: '',
            inputRules: [
                v => !!v || 'Tag is required',
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
            addTag() {
                if(this.$refs.form.validate()){
                    let checkTag = this.tags.find(x=> x.tag == this.tag);
                    if(checkTag){
                        this.snackbarText= 'Tag Already Exist';
                        this.snackbar= true; 
                    }
                    else{
                        this.snackbarText= 'Tag Added Successfully';
                        this.snackbar= true; 
                        this.$refs.form.reset(); 
                    }
                }
            },
            reset () {
                this.$refs.form.reset()
            },
        },
    }
</script>