<template>
  <div class="home">
    <b-card-header><h5>Übersicht</h5></b-card-header>
    <b-card-body>
        <formular-summary v-for="(formular, index) in formulare" :key="formular.title" :formular="formular" :index="index"/>
    </b-card-body>
  </div>
</template>

<script>
// @ is an alias to /src
import formulareImport from  "@/formulare"
import FormularSummary from "@/components/formularSummary";

export default {
  name: 'Home',
  components: {
    FormularSummary
  },
  computed: {
    formulare: ()=> formulareImport
  }
}
</script>
