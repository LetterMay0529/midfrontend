<template>
    <div>
        <NavBar />
        <EditListingModal :listing="selectedListing" />
        <DeleteListingModal :listing="selectedListing" @onDeleted="getAll"/>
        <div class="container">
            <h1>
                Property Listings
                <ListingEntry class="float-right" @onAdd="getAll"/>
            </h1>

            <table class="table table-bordered table-stripped">
                <thead>
                    <tr class="bg-info text-white">
                        <th>Property Type</th>
                        <th>Category</th>
                        <th>Location</th>
                        <th>Value</th>
                        <th>Description</th>
                        <th>Date Acquired</th>
                        <th>&nbsp;</th>
                        <th>&nbsp;</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="listing in listings" :key="listing.id">
                        <td>{{listing.prop_type}}</td>
                        <td>{{listing.prop_category}}</td>
                        <td>{{listing.location}}</td>
                        <td>{{listing.value}}</td>
                        <td>{{listing.description}}</td>
                        <td>{{listing.acquired_on}}</td>
                        
                        <td>
                            <b-button @click="onEdit(listing)" variant="info" size="sm">
                                Edit
                            </b-button>
                        </td>
                        <td>
                            <b-button @click="onDelete(listing)" variant="danger" size="sm">
                                Delete
                            </b-button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
export default {
    
    data() {
        return {
            listings: [],
            selectedListing: {}
        }
    },
    methods: {
        async getAll() {
            await this.$axios.get('/api/listings')
            .then((res)=>{
                if(res.status==200) {
                    this.listings =res.data
                }
            })
        },
        onEdit(selectedListing) {
            this.selectedListing = selectedListing;
            this.$bvModal.show('editListingModal')
        },
        onDelete(selectedListing) {
            this.selectedListing = selectedListing;
            this.$bvModal.show('deleteListingModal')
        }
    },
    created() {
        this.getAll()
    }
}
</script>