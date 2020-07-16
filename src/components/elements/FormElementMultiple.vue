<template>
  <fieldset class="field">
    <p class="mb-1" v-if="schema.title">{{ schema.title }}</p>
    <p v-if="schema.description" class="text-muted">{{schema.description}}</p>
    <hr>
    <div v-for="(item, index) in items" class="columns" :key="index">
      <div class="column">
        <form-element :schema="schema.items" :value="item" @input="updateValue($event, index)"></form-element>
        <b-button class="ml-3 mt-n3 mb-3" type="button" variant="danger" v-if="items.length > 0" @click="items.splice(index, 1)" :key="`remove-${index}`">Entfernen</b-button>
      </div>
    </div>
      <b-button type="button" class="button" variant="success" @click="addItem()">Hinzufügen</b-button>
  </fieldset>
</template>

<script>
import { scaffoldFromSchema } from '@/utility/json-schema-helpers'
export default {
  name: 'FormElementMultiple',
  components: {
    // load at runtime to avoid circular dependency https://vuejs.org/v2/guide/components-edge-cases.html#Circular-References-Between-Components
    FormElement: () => import('@/components/elements/FormElement')
  },
  props: [
    'schema',
    'value'
  ],
  data () {
    return {
      items: (this.value !== undefined) ? this.value : scaffoldFromSchema(this.schema)
    }
  },
  methods: {
    addItem() {
      this.items.push(scaffoldFromSchema(this.schema)[0])
    },
    updateValue (value, index) {
      this.items.splice(index, 1, value)
      this.$emit('input', this.items)
    }
  }
}
</script>

<style scoped>
  fieldset {
    padding: 10px;
    border: none;
    border-left: 4px solid #ddd;
  }
  fieldset > legend {
    font-weight: bold;
  }
</style>
