<template>
    <div>

        <b-card-body>
            <schema-form v-model="model" :schema="form" @submit="submit"/>
        </b-card-body>
    </div>
</template>

<script>
    import formInput from "@/formular1.json"
    import schemaForm from "../components/SchemaForm"
    export default {
        name: "Formular",
        components: {schemaForm},
        data() {
            return {
                model: {}
            }
        },
        computed:{
            form: () => formInput
        },
        methods: {
            submit() {
                console.log("gesendet")
            }
        },
    }
</script>

<style lang="scss">
    @import "../styles";
    input {
        @extend .form-control
    }
</style>
