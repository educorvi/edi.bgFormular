<template>
    <b-form @submit.prevent="submit" class="text-left">
        <slot name="header" :error-messages="activeErrorMessages">
            <b-alert
                    :show="activeErrorMessages.length>0"
                    variant="danger"
                    :closable="false"
                    id="error-messages">
                <div v-for="(error, index) in activeErrorMessages" :key="index">
                    <div>{{ error }}</div>
                </div>
            </b-alert>
        </slot>
        <template v-for="(property, key) in schema.properties">
            <slot :name="key" :item="{key: key, schema: property, value: items[key], update: updateValue}">
                <div :key="key">
                    <component :is="element" :schema="property" :value="items[key]"
                               @input="updateValue($event, key)"></component>
                    <hr>
                </div>
            </slot>
        </template>
        <slot name="actions">
            <div class="control w-100">
                <b-button variant="danger" to="/" class="float-left mb-3">Abbrechen</b-button>
                <b-button type="submit" variant="primary" class="float-right mb-3"><span>Senden</span></b-button>
            </div>
        </slot>
    </b-form>
</template>

<script>
    import Ajv from 'ajv'
    import JSONPointer from 'json-pointer'
    import FormElement from '@/components/elements/FormElement'
    import {scaffoldFromSchema, pruneEmptyMembers} from '@/utility/json-schema-helpers'

    let ajv = new Ajv({allErrors: true, jsonPointers: true, format: 'full'})

    export default {
        name: 'SchemaForm',
        components: {
            FormElement
        },
        props: {
            schema: {
                type: Object
            },
            value: {
                type: Object
            },
            element: {
                default() {
                    return 'form-element'
                }
            }
        },
        data() {
            return {
                items: (this.value !== undefined) ? this.value : scaffoldFromSchema(this.schema),
                activeErrorMessages: [],
            }
        },
        watch: {
            schema() {
                this.items = scaffoldFromSchema(this.schema)
                ajv = new Ajv({allErrors: true, jsonPointers: true, format: 'full'})
            }
        },
        methods: {
            submit() {
                if (this.validate()) {
                    this.activeErrorMessages = []
                    this.$emit('input', pruneEmptyMembers(this.items))
                    this.$emit('submit')
                } else {
                    this.buildErrors()
                    scrollTo(0,0)
                }
            },
            validate() {
                // validate against schema
                return ajv.validate(this.schema, pruneEmptyMembers(this.items))
            },
            buildErrors() {
                this.activeErrorMessages = ajv.errors.map((error) => {
                    if (error.keyword === 'required') {
                        const path = error.dataPath.length === 0 ? `/properties/${error.params.missingProperty}` : error.schemaPath.substring(1, error.schemaPath.length - 8) + `properties/${error.params.missingProperty}`
                        const property = JSONPointer.get(this.schema, path)
                        return property.title + ' muss ausgefüllt werden'
                    } else if (error.keyword === 'format') {
                        const path = error.schemaPath.substring(1, error.schemaPath.length - 7)
                        const property = JSONPointer.get(this.schema, path)
                        return `${property.title} ist nicht im richtigen Format. Bsp: ${property.example}`
                    } else if (error.keyword === 'pattern') {
                        const path = error.schemaPath.substring(1, error.schemaPath.length - 8)
                        const property = JSONPointer.get(this.schema, path)
                        return `${property.title} ist nicht im richtigen Format. Bsp:  ${property.example}`
                    }
                })
            },
            updateValue(value, child) {
                this.items[child] = value
            }
        }
    }
</script>
