<template>
  <b-form-group :label="schema.title" :label-for="schema.title" :description="schema.description">
    <b-datepicker :value="value" @input="$emit('input', $event)" placeholder="Klicken um ein Datum auszuwählen">
    </b-datepicker>
  </b-form-group>
</template>

<script>
export default {
  name: 'DatePickerElement',
  props: [
    'schema',
    'value'
  ]
}
</script>
