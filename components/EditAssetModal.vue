<template>
    <div>
        
        <b-modal id="editAssetModal" title="Asset Entry" ok-title="Save Asset" @ok="onSubmit">
            <form action="#">
                <b-form-group
                    label="Name"
                    label-for="name"
                >
                <b-form-input id="name" v-model="asset.name" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Description"
                    label-for="description"
                >
                <b-form-input id="description" v-model="asset.description" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Location"
                    label-for="location"
                >
                <b-form-input id="location" v-model="asset.location" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Value"
                    label-for="value"
                >
                <b-form-input id="value" v-model="asset.value" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Date Acquired"
                    label-for="acquired_on"
                >
                <b-form-input id="acquired_on" type="date" v-model="asset.acquired_on" trim></b-form-input>
                </b-form-group>

                <b-form-group
                    label="Status"
                    label-for="status"
                >
                <b-form-select v-model="asset.status" :options="statuses"></b-form-select>
                </b-form-group>
            </form>
        </b-modal>
    </div>
</template>

<script>
export default {
    props: {
        asset: {}
    },
    data() {
        return {
            statuses: [
                {value: 'good', text: 'In good condition'},
                {value: 'damaged', text: 'Damaged'},
                {value: 'lost', text: 'Lost'},
            ]
        }
    },
    methods: {
        async onSubmit() {
            this.$axios.put('/api/assets/'+this.asset.id, this.asset)
            .then((res)=>{
                if(res.status==202) {
                    alert('Update successfully!')
                }
            })
            .catch((err)=> {
                alert(err.message)
            })
        }
    }
}
</script>