<template>
    <div>
        <div
            class="title-text mb-5"
        >
            Add New Venue Category
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
        name: 'AddNewVenueCategory',
        data: ()=>({
            valid: true,
            category: '',
            inputRules: [
                v => !!v || 'Category is required',
            ],
            categories: [
                {
                    id: 1, 
                    cat: 'Art', 
                },
                {
                    id: 2, 
                    cat: 'Business', 
                },
                {
                    id: 3, 
                    cat: 'Concert', 
                },
                {
                    id: 4, 
                    cat: 'Conferrence', 
                },
                {
                    id: 5, 
                    cat: 'Education', 
                },
                {
                    id: 6, 
                    cat: 'Festival', 
                },
                {
                    id: 7, 
                    cat: 'Food', 
                },
                {
                    id: 8, 
                    cat: 'Micellaneous', 
                },
                {
                    id: 9, 
                    cat: 'Nightlife', 
                },
                {
                    id: 10, 
                    cat: 'Sports', 
                },
                {
                    id: 11, 
                    cat: 'Technology', 
                },
                {
                    id: 12, 
                    cat: 'Travel', 
                },
                {
                    id: 13, 
                    cat: 'Wedding', 
                },
            ],
            snackbar: false,
            snackbarText: '' , 
        }),
        methods: {
            addCategory() {
                if(this.$refs.form.validate()){
                    let checkCategory = this.categories.find(x=> x.cat == this.category);
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