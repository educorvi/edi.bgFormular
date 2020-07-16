<template>
    <div>
        <b-card-body v-if="schema">
            <schema-form  v-model="model" :schema="schema" @submit="submit"/>
        </b-card-body>
        <custom-spinner v-else/>
    </div>
</template>

<script>
    import formInput from "@/formulare.json"
    import schemaForm from "../components/SchemaForm"
    import CustomSpinner from "@/components/CustomSpinner";
    export default {
        name: "Formular",
        components: {CustomSpinner, schemaForm},
        data() {
            return {
                model: {},
                schema: {}
            }
        },
        created() {
            this.schema = formInput.formulare[this.$route.params.id];
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
