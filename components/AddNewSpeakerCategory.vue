<template>
    <div>
        <div
            class="title-text mb-5"
        >
            Add New Category
        </div>
        <div>           
            <v-form
                ref="form"
                v-model="valid"
                lazy-validation
            >
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
                    @click="addCategory"
                    elevation="0"
                >
                    Add Category
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
        name: 'AddNewSpeakerCategory',
        data: ()=>({
            valid: true,
            category: '',
            inputRules: [
                v => !!v || 'Category is required',
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
            snackbar: false,
            snackbarText: '' , 
        }),
        methods: {
            addCategory() {
                if(this.$refs.form.validate()){
                    let checkCategory = this.categories.find(x=> x.category == this.category);
                    if(checkCategory){
                        this.snackbarText= 'Category Already Exist';
                        this.snackbar= true; 
                    }
                    else{
                        this.snackbarText= 'Category Added Successfully';
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