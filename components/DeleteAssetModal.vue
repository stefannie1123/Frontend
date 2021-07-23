<template>
    <div>

        <b-modal id="deleteAssetModal" title="Delete Asset" ok-title="Delete" @ok="onDelete" ok-variant="danger">
            Are You Sure about deleting this asset?<br><br>
            <h2>{{asset.name}}</h2> 
            <h5>- {{asset.description}}</h5>
        </b-modal>
    </div>
</template>

<script>
export default {
    props: {
        asset: {}
    },
    methods: {
        async onDelete(){
            this.$axios.delete('/api/assets/' + this.asset.id)
            .then((res)=>{
                if(res.status==202) {
                    alert('Asset is deleted successfully')
                    this.$emit('onDeleted')
                }
            })
        }
    }
}
</script>