<template>
  <div class="add container">
    <Alert v-if="alert" v-bind:message="alert" />
    <h1 class="page-header">Add Customer</h1>
    <form v-on:submit="addCustomer">
      <div class="well">
        <h4>Customer Info</h4>
        <div class="form-group">
          <label>First Name</label>
          <input type="text" class="form-control" placeholder="First Name" v-model="customer.firstName">
        </div>
        <div class="form-group">
          <label>Last Name</label>
          <input type="text" class="form-control" placeholder="Last Name" v-model="customer.lastName">
        </div>
      </div>
      <div class="well">
        <h4>Customer Contact</h4>
        <div class="form-group">
          <label>Email</label>
          <input type="text" class="form-control" placeholder="Email" v-model="customer.email">
        </div>
        <div class="form-group">
          <label>Phone</label>
          <input type="text" class="form-control" placeholder="Phone" v-model="customer.phone">
        </div>
      </div>

      <div class="well">
        <h4>Customer Location</h4>
        <div class="form-group">
          <label>City</label>
          <input type="text" class="form-control" placeholder="City" v-model="customer.city">
        </div>
        <div class="form-group">
          <label>Street</label>
          <input type="text" class="form-control" placeholder="Street" v-model="customer.street">
        </div>
        <div class="form-group">
          <label>House</label>
          <input type="text" class="form-control" placeholder="House" v-model="customer.house">
        </div>
      </div>
      <button type="submit" class="btn btn-primary">Submit</button>
    </form>
    <br />
    <br />
  </div>
</template>

<script>
  import Alert from './Alert.vue'
  export default {
    name: 'add',
    data() {
      return {
        customer: {},
        alert: ''
      }
    },
    methods: {
      addCustomer(e) {
        if (!this.customer.firstName || !this.customer.lastName || !this.customer.email) {
          this.alert = "Please fill the required fields"
        } else {
          this.$http.post("http://localhost:8080/customer/add", this.customer)
            .then(function (response) {
              this.$router.push({path: '/', query: {alert: 'Customer Added'}})
            });
          e.preventDefault()
        }
        e.preventDefault()
      }
    },
    components: {
        Alert
    }
  }
</script>

<style scoped>

</style>
