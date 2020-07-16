<template>
  <div id="app">
    <Headbar/>
    <div class="container-fluid pt-3 pb-3" id="view">
      <b-card no-body>
        <router-view/>
      </b-card>
    </div>
  </div>
</template>

<style lang="scss">
  @import "styles";
  #app {
    background-color: $primary;
    text-align: center;
  }
  #view {
    max-width: 800px;
    margin-bottom: 10px;
  }
</style>
<script>
  import Headbar from "@/components/Headbar";
  export default {
    components: {Headbar}
  }
</script>
