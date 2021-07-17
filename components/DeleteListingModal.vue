<template>
    <div>
        <b-modal id="deleteListingModal" title="Listing Entry" ok-title="Delete Listing" @ok="onDelete" ok-variant="danger">
            Are you sure you want to delete this listing? <br>
            {{listing.prop_type}} {{listing.prop_category}}
        </b-modal>
    </div>
</template>
<script>
export default {
    props: {
        listing: {}
    },
    methods: {
        async onDelete() {
            this.$axios.delete('/api/listings/'+this.listing.id)
            .then((res)=>{
                if(res.status==202) {
                    alert('Listing deleted')
                    this.$emit('onDeleted')
                }
            })
        }
    }
}
</script>