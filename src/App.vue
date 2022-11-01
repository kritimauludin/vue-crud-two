<template>
  <div id="app">
    <div class="container">
      <h1 class="mb-4">Daftar Siswa</h1>
      <hr />
      <p>
        <button
          class="btn btn-dark"
          type="button"
          data-toggle="collapse"
          data-target="#collapseExample"
          aria-expanded="false"
          aria-controls="collapseExample"
        >
          + Siswa
        </button>
      </p>

      <customer-table
        v-bind:customers="customers"
        @edit-customer="editCustomer"
        @delete-customer="deleteCustomer"
      />

      <div class="collapse" id="collapseExample">
        <div class="card card-body">
          <h2>Input Data Pelanggan</h2>
          <hr />

          <!-- <customer-form @add-customer="addCustomer"/> -->
          <customer-form @add-customer="addCustomer" />
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import CustomerTable from "@/components/CustomerTable.vue";
import CustomerForm from "@/components/CustomerForm.vue";

export default {
  name: "App",
  components: {
    CustomerTable,
    CustomerForm,
  },
  data() {
    return {
      customers: [
        {
          id: 1,
          name: "Fahmi",
          email: "fahmi123@mail.com",
          address: "jl.semangat",
        },
        {
          id: 2,
          name: "Arik",
          email: "arik321@mail.com",
          address: "jl.pahlawan",
        },
        {
          id: 3,
          name: "Yayan",
          email: "yayan123@mail.com",
          address: "jl.imam bonjol",
        },
      ],
    };
  },
  methods: {
    addCustomer(customer) {
      this.customers.push(customer);
    },
    editCustomer(id, data) {
      this.customers = this.customers.map(function (customer) {
        return customer.id === id ? data : customer;
      });
    },
    deleteCustomer(id) {
      this.customers = this.customers.filter(function (customer) {
        return customer.id !== id;
      });
    },
  },
};
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
