<template>
    <div>
        <NavBar />
        <EditAssetModal :asset="selectedAsset"/>
        <DeleteAssetModal :asset="selectedAsset" @onDeleted="getAll"/>
        <div class="container">
            <h1>
                Assets
                <AssetEntryModal class="float-right" @onAdd="getAll"/>
            </h1>
            <table class="table table-bordered table-striped">
                <thead>
                    <tr class="bg-info text-white">
                        <th>Name</th>
                        <th>Description</th>
                        <th>Location</th>
                        <th>Value</th>
                        <th>Status</th>
                        <th>&nbsp;</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="asset in assets" :key="asset.id">
                        <td>{{asset.name}}</td>
                        <td>{{asset.description}}</td>
                        <td>{{asset.location}}</td>
                        <td>{{asset.value}}</td>
                        <td>{{asset.status}}</td>
                        <td>
                            <b-button @click="onEdit(asset)" variant="info" size="sm">
                                Edit
                            </b-button>
                            <b-button @click="onDelete(asset)" variant="danger" size="sm">
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
            assets: [],
            selectedAsset: {}
        }
    },
    methods: {
        async getAll() {
            await this.$axios.get('/api/assets')
            .then((res)=>{
                if(res.status==200) {
                    this.assets = res.data
                    console.log(this.assets)
                }
            })
        },
        onEdit(selectedAsset) {
            this.selectedAsset = selectedAsset;
            this.$bvModal.show('editAssetModal')
        },
        onDelete(selectedAsset) {
            this.selectedAsset = selectedAsset;
            this.$bvModal.show('deleteAssetModal')
        }
    },
    created() {
        this.getAll()
    }
}
</script>