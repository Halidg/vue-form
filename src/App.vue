<template>
  <div class="container">
    <vue-form></vue-form> 
  </div>
  
</template>

<script>
import VueForm from './components/VueForm.vue'

export default {
  components: {VueForm}  
}
</script>

<style lang="scss" scoped>
.container {
 margin: 0 auto;
 max-width: 900px;
 padding: 15px;  
}
</style>
