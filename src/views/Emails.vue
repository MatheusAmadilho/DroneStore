<template>
  <div>
    <div class="main-container">
      <h1>Emails cadastrados:</h1>
      <Dashboard />
    </div>
  </div>
</template>

<script>
import Dashboard from '../components/Dashboard'

export default {
  name: 'Emails',
  components: {
    Dashboard
  }
}
</script>

<style scoped>
h1 {
  width: 500px;
  font-size: 50px;
  margin: auto;
  margin-top: 30px;
  margin-bottom: 30px;
}

</style>

