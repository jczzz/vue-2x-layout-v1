<template>
<main>
<CustomerList />
</main>
  
</template>

<script>
import CustomerList from './components/CustomerList.vue'


export default {
  name: 'App',
  components: {
    CustomerList
  }
}
</script>

<style>
body {
  background: #F2F5FA;
}
main {
  padding-top:30px;
}

</style>
