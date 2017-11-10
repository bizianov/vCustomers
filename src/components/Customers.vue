<template>
  <div class="customers container">
    <Alert v-if="alert" v-bind:message="alert" />
    <h1 class="page-header">Manage Customers</h1>
    <input class="form-control" placeholder="Type Last Name" v-model="filterInput"/>
    <br />
    <table class="table table-striped">
      <thead>
      <tr>
        <th>First Name</th>
        <th>Last Name</th>
        <th>Phone</th>
        <th>Email</th>
        <th></th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="customer in filterBy(customers, filterInput)">
        <td>{{customer.firstName}}</td>
        <td>{{customer.lastName}}</td>
        <td>{{customer.phone}}</td>
        <td>{{customer.email}}</td>
        <td><router-link v-bind:to="'/customer/' + customer.id" class="btn btn-default">View</router-link></td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  import Alert from './Alert.vue'
  export default {
    name: 'customers',
    data() {
      return {
        customers: [],
        filterInput: '',
        alert: ''
      }
    },
    methods: {
      fetchCustomers() {
        this.$http.get('http://localhost:8080/customers')
          .then(function (response) {
            this.customers = response.body
          })
      },
      filterBy(list, value) {
          value = value.charAt(0).toUpperCase() + value.slice(1);
          return list.filter(function (customer) {
            return customer.lastName.indexOf(value) > -1
          })
      }
    },
    created: function() {
      if (this.$route.query.alert) {
          this.alert = this.$route.query.alert
      }
      this.fetchCustomers();
    },
    components: {
        Alert
    }
  }
</script>

<style scoped>

</style>
