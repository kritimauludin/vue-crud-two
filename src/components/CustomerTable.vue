<template>
  <div class="customer-table">
    <table class="table table-bordered">
      <thead class="thead-light">
        <tr>
          <th scope="col" class="text-center">Nama</th>
          <th scope="col" class="text-center">Email</th>
          <th scope="col" class="text-center">Alamat</th>
          <th scope="col" class="text-center">Tindakan</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="customer in customers" :key="customer.id">
          <template v-if="customerId === customer.id">
            <td>
              <label for="name" class="font-weight-bold">Nama:</label>
              <div>
                <input
                  type="text"
                  v-model="customer.name"
                  class="form-control"
                />
              </div>
            </td>
            <td>
              <label for="email" class="font-weight-bold">Email:</label>
              <div>
                <input
                  type="text"
                  v-model="customer.email"
                  class="form-control"
                />
              </div>
            </td>
            <td>
              <label for="address" class="font-weight-bold">Address:</label>
              <div>
                <input
                  type="text"
                  v-model="customer.address"
                  class="form-control"
                />
              </div>
            </td>
            <td>
              <div class="mt-4">
                <button
                  class="btn btn-success mr-2"
                  @click="saveEdit(customer)"
                >
                  Simpan
                </button>
                <button class="btn btn-danger" @click="cancelEdit(customer)">
                  Batal
                </button>
              </div>
            </td>
          </template>
          <template v-else>
            <td class="text-center">{{ customer.name }}</td>
            <td class="text-center">{{ customer.email }}</td>
            <td class="text-center">{{ customer.address }}</td>
            <td>
              <div class="text-center">
                <button
                  class="btn btn-warning mr-2"
                  @click="editCustomer(customer)"
                >
                  Ubah
                </button>
                <button
                  class="btn btn-danger"
                  @click="deleteCustomer(customer.id)"
                >
                  Hapus
                </button>
              </div>
            </td>
          </template>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "customer-table",
  props: {
    customers: Array,
  },
  data() {
    return {
      customerId: null,
    };
  },
  methods: {
    editCustomer(customer) {
      this.data = Object.assign({}, customer);
      this.customerId = customer.id;
      // console.log(this.data);
    },
    saveEdit(customer) {
      let id = this.data.id;
      this.$emit("edit-customer", id, customer);
      this.customerId = null;
    },
    cancelEdit(customer) {
      Object.assign(customer, this.data);
      this.customerId = null;
      // console.log(this.customerId);
    },
    deleteCustomer(id) {
      this.$emit("delete-customer", id);
    },
  },
};
</script>

<style scoped>
</style> 