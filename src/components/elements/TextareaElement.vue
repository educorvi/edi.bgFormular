<template>
  <b-form-group :label="schema.title" :label-for="schema.title" :description="schema.description">
    <b-form-textarea type="textarea" :minlength="schema.minLength" :maxlength="schema.maxLength" :value="value" @input="$emit('input', $event)">
    </b-form-textarea>
  </b-form-group>
</template>

<script>
export default {
  name: 'TextareaElement',
  props: [
    'schema',
    'value'
  ]
}
</script>
