<template>
  <b-form-group :label="schema.title" :label-for="schema.title" :description="schema.description">
    <b-input type="number" :min="schema.minimum" :max="schema.maximum" :step="schema.type === 'number' ? 'any': '1'" :value="value" @input="$emit('input', Number($event))">
    </b-input>
  </b-form-group>
</template>

<script>
export default {
  name: 'NumberElement',
  props: [
    'schema',
    'value'
  ]
}
</script>
