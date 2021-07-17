<template>
    <div>
        <b-button v-b-modal.listingEntryModal variant="primary " >Add Listing</b-button>

        <b-modal id="listingEntryModal" title="Listing Entry" ok-title="Save Listing" @ok="onSubmit">
           <form action="#" >
                              <b-form-group
                label="Property Type "
                label-for="prop_type"
                >
                <b-form-select v-model="listing.prop_type" :options="types"></b-form-select>
                </b-form-group>

                 <b-form-group
                label="Category "
                label-for="prop_category"
                >
                <b-form-select v-model="listing.prop_category" :options="categories"></b-form-select>
                </b-form-group>

                 <b-form-group
                label="Location"
                label-for="location"
                >
                <b-form-input id="location" v-model="listing.location"  trim></b-form-input>
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
                <b-form-input id="description" v-model="listing.description"  trim></b-form-input>
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
    data() {
        return {
            listing: {},
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
            this.$axios.post('/api/listings', this.listing)
            .then((res)=>{
                if(res.status==202) {
                    alert('Listing successfully added')
                    this.$emit('onAdd')
                }
            })
        }
    }
}
</script>