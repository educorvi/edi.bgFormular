<template>
    <div class="field">
<!--        <b-form-radio-group :label="schema.title">-->
<!--            <div v-for="(item, index) in schema.anyOf" class="field radio-field" :key="index">-->
<!--                <b-form-radio :value="value" @input="$emit('input', $event)" :native-value="item.enum[0]">-->
<!--                    <span class="radio-title">{{ item.title }}</span>-->
<!--                </b-form-radio>-->
<!--            </div>-->
<!--        </b-form-radio-group>-->
        <b-alert variant="warning" show>"Anyof" not yet implemented. Field "{{schema.title}}" could not be rendered</b-alert>
    </div>
</template>

<script>
    export default {
        name: 'RadioButtonElement',
        props: [
            'schema',
            'value'
        ]
    }
</script>

<style scoped>
    .radio-field {
        padding-left: 15px;
    }

    .radio-title {
        display: block;
        padding-left: 10px;
    }
</style>
