<template>
    <div>
        <b-form-group
            id="input-group-1"
            label="Subject"
            label-for=""
            description=""
        >
            <b-form-input
                type="text"
                :value="subject(row.Name)"
            ></b-form-input>
        </b-form-group>

        <b-form-group>
            <b-form-textarea
                id="textarea"
                placeholder="Enter something..."
                rows="3"
                max-rows="6"
                :value="message(row.Company,row.Name)"
            ></b-form-textarea>
        </b-form-group>
    </div>
</template>

<script>
export default {
    data(){
        props: ['csv_data']
        return {
            row : {}
        }
    },
    mounted(){
        this.row = this.$attrs.csv_data
    },
    methods:{
        subject(name){
            if(name) return `Hello ${name}`
            return ''
        },
        message(company,name){
            if(company) return `How are you at ${$company}?`
            return `${name}, how are things?`
        }
    }
}
</script>

<style>

</style>
