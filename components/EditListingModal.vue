<template>
    <div>
        <b-modal id="editListingModal" title="Listing Entry" ok-title="Save Listing" @ok="onSubmit">
            <form action="#">
                 <b-form-group
                label="Property Type"
                label-for="type"
                >
                <b-form-select v-model="listing.prop_type" :options="types"></b-form-select>
                </b-form-group>

                <b-form-group
                label="Category"
                label-for="category"
                >
                <b-form-select v-model="listing.prop_category" :options="categories"></b-form-select>
                </b-form-group>

                <b-form-group
                label="Location"
                label-for="location"
                >
                <b-form-input id="location" v-model="listing.location" trim></b-form-input>
                </b-form-group>

                <b-form-group
                label="Value"
                label-for="value"
                >
                <b-form-input id="value" v-model="listing.value" trim></b-form-input>
                </b-form-group>

                <b-form-group
                label="Description"
                label-for="description"
                >
                <b-form-input id="description" v-model="listing.description" trim></b-form-input>
                </b-form-group>

                <b-form-group
                label="Date Acquired"
                label-for="acquired_on"
                >
                <b-form-input id="acquired_on" type="date" v-model="listing.acquired_on" trim></b-form-input>
                </b-form-group>

            </form>
        </b-modal>
    </div>
</template>
<script>
export default {
    props: {
        listing: {}
    },
    data() {
        return {

        types: [
                {value: 'For Sell', text: 'For Sell'},
                {value: 'For Rent', text: 'For Rent'},
                {value: 'Foreclosure', text: 'Foreclosure'},
            ],

            categories: [
                {value: 'Residential', text: 'Residential'},
                {value: 'Commercial', text: 'Commercial'},
                {value: 'Land', text: 'Land'},
            ]         
        }
    },
    methods: {
        async onSubmit() {
            this.$axios.put('/api/listings/'+this.listing.id, this.listing)
                .then((res)=>{
                    if(res.status==202) {
                        alert('Update successfully!!')
                    }
                })
                .catch((err)=> {
                    alert(err.message)
                })
        }
    }
}
</script>