<template>
  <div class="details container">
    <router-link to="/">Back</router-link>
    <h1 class="page-header">{{currentCustomer.firstName}} {{currentCustomer.lastName}}
      <span class="pull-right">
        <button class="btn btn-danger" v-on:click="deleteCustomer(currentCustomer.id)">Delete</button>
        <router-link v-bind:to="'/edit/' + currentCustomer.id" class="btn btn-default">Edit</router-link>
      </span>
    </h1>

    <ul class="list-group">
      <li class="list-group-item"><span class="glyphicon glyphicon-phone" aria-hidden="true"></span> {{currentCustomer.phone}}</li>
      <li class="list-group-item"><span class="glyphicon glyphicon-envelope" aria-hidden="true"></span> {{currentCustomer.email}}</li>
    </ul>

    <ul class="list-group">
      <li class="list-group-item"> {{currentCustomer.city}}</li>
      <li class="list-group-item">{{currentCustomer.street}}</li>
      <li class="list-group-item">{{currentCustomer.house}}</li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'details',
    data() {
      return {
        currentCustomer: {}
      }
    },
    methods: {
      fetchCustomer(id) {
        return this.$http.get("http://localhost:8080/customer/" + id)
          .then(function (response) {
            this.currentCustomer = response.body
          })
      },
      deleteCustomer(id) {
          return this.$http.delete("http://localhost:8080/customer/delete/" + id)
            .then(function (response) {
              this.$router.push({path: '/', query: {alert: 'User Deleted'}})
            })
      }
    },
    created: function(){
        this.fetchCustomer(this.$route.params.id);
    }
  }
</script>

<style scoped>

</style>
