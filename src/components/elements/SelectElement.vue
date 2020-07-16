<template>
  <b-form-group :label="schema.title" :label-for="schema.title" :description="schema.description">
    <b-form-select :value="value" @input="$emit('input', $event)" :placeholder="schema.title">
      <option v-for="item in schema.enum" :value="item" :key="item">
        {{ item }}
      </option>
    </b-form-select>
  </b-form-group>
</template>

<script>
export default {
  name: 'SelectElement',
  props: [
    'schema',
    'value'
  ]
}
</script>
