<template>
    <div>
      <Banner />
      <div class="main-container">
        <h1>Monte o seu café:</h1>
        <CafeForm />
      </div>
    </div>
  </template>
  
  <script>
  import Banner from '../components/Banner'
  import CafeForm from '../components/CafeForm.vue'
  export default {
    name: 'Home',
    components: {
      Banner,
      CafeForm
    }
  }
  </script>