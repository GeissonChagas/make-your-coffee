<template>
  <Banner />
  <div class="main-container">
    <h1>Faça suas escolhas:</h1>
    <CoffeeForm />
  </div>
</template>

<script>
  import Banner from '../components/Banner.vue'
  import CoffeeForm from '../components/CoffeeForm.vue'

  export default{
    name: "Home",
    components: {
      Banner,
      CoffeeForm
    }
  }

</script>

<style>
  
</style>
