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
                :value="subject(row.name)"
            ></b-form-input>
        </b-form-group>

        <b-form-group>

            <b-form-textarea
                id="textarea"
                placeholder="Enter something..."
                rows="3"
                max-rows="6"
                :value="message(row)"
            ></b-form-textarea>
        </b-form-group>
    </div>
</template>

<script>
export default {
    data(){
        props: ['csv_data']
        return {
            row : [],
            log : {},
        }
    },
    mounted(){
        this.row = this.$attrs.csv_data
        this.row = JSON.stringify(this.row).replace(/[\\r]+/g, '').toLowerCase() // clean the object
        this.row = JSON.parse(this.row)
    },
    methods:{
        subject(name){
            if(name) return `Hello ${this.properCase(name)}`
            return ''
        },
        message(row){
            // this.properCase(row.name)
            if(row.company) return `How are you at ${this.properCase(row.company)}?`
            return `${this.properCase(row.name)}, how are things?`
        },
        properCase(string) {
            console.log(string)
            if(string == "" || !string || string == undefined) return false
            let new_string = ""
            string.split(" ").forEach(element => {
                new_string += element.charAt(0).toUpperCase() + element.slice(1) + " "
            })
            return new_string
        }
    },
    filters : {
    }
}
</script>

<style>

</style>
