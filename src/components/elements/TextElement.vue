<template>
  <b-form-group :label="schema.title" :label-for="schema.title" :description="schema.description">
    <b-form-input :id="schema.title" :value="value" @input="$emit('input', $event)" :placeholder="schema.example">
    </b-form-input>
  </b-form-group>
</template>

<script>
export default {
  name: 'TextElement',
  props: [
    'schema',
    'value'
  ]
}
</script>
