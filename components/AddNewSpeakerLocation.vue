<template>
    <div>
        <div
            class="title-text mb-5"
        >
            Add New Location
        </div>
        <div>           
            <v-form
                ref="form"
                v-model="valid"
                lazy-validation
            >
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
                    @click="addLocation"
                    elevation="0"
                >
                    Add Location
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
        name: 'AddNewSpeakerLocation',
        data: ()=>({
            valid: true,
            location: '',
            inputRules: [
                v => !!v || 'Location is required',
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
            snackbar: false,
            snackbarText: '' , 
        }),
        methods: {
            addLocation() {
                if(this.$refs.form.validate()){
                    let checkLocation = this.locations.find(x=> x.location == this.location);
                    if(checkLocation){
                        this.snackbarText= 'Location Already Exist';
                        this.snackbar= true; 
                    }
                    else{
                        this.snackbarText= 'Location Added Successfully';
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