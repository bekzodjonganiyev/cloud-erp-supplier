<template>
  <Layout>
    <h1 class="font-semibold text-xl">Customers</h1>
    <div class="my-5">
      <div class="flex">
        <label class="relative block">
          <!-- <span class="sr-only">Search</span> -->
          <span class="absolute left-1 top-2 flex items-center pl-2">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-5 w-5 text-slate-400"
              viewBox="0 0 20 20"
              fill="currentColor"
            >
              <path
                fill-rule="evenodd"
                d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z"
                clip-rule="evenodd"
              />
            </svg>
          </span>
          <input
            class="placeholder:text-slate-400 block bg-white w-96 rounded-md py-2 pl-9 pr-3 shadow-sm focus:outline-none focus:border-sky-500 focus:ring-sky-500 focus:ring-1 sm:text-sm"
            placeholder="Search customer"
            type="text"
            name="search"
          />
        </label>
        <div class="inline-flex justify-end ml-80">
          <div class="flex mr-5">
            <img class="w-7 h-7 fill-blue-900 mt-2 rotate-180" src="../../assets/export.svg" alt />
            <button class="text-indigo-600">Import</button>
          </div>
          <div class="flex mr-5">
            <img class="fill-blue-900 w-7 h-7 mt-2 text-blue-900" src="../../assets/export.svg" alt />
            <button class="text-indigo-600">Export</button>
          </div>
          <div>
            <router-link to="/customers/create">
              <button
                class="bg-blue-800 text-white active:bg-blue-400 font-bold text-sm px-6 py-3 rounded shadow hover:shadow-lg outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150"
                type="button"
              >Add Customers</button>
            </router-link>
          </div>
        </div>
      </div>
      <div class="h-full w-full">
        <h1 class="text-xl my-6">Recent Customers</h1>
        <div class="overflow-auto p-5 bg-white rounded-lg shadow hidden md:block">
          <table class="w-full">
            <thead class="bg-gray-100">
              <tr>
                <th
                  class="w-32 text-zinc-400 p-3 text-sm font-semibold tracking-wide text-left"
                >Customer Name</th>
                <th
                  class="w-32 text-zinc-400 p-3 text-sm font-semibold tracking-wide text-left"
                >Phone Number</th>
                <th
                  class="w-32 text-zinc-400 p-3 text-sm font-semibold tracking-wide text-left"
                >Options</th>
              </tr>
            </thead>
            <tbody class="divide-y divide-gray-100">
              <tr v-for="(customer, index) in customers" :key="index" class="bg-white">
                <td class="p-3 text-sm text-gray-700 whitespce-nowrap">{{ customer.name }}</td>
                <td class="p-3 text-sm text-gray-700 whitespce-nowrap">{{ customer.phone }}</td>
                <td class="flex">
                  <button type="button" class="mr-2 bg-orange-400 py-1 px-2 rounded">
                    <RouterLink :to="{ name: 'customers.edit', params: { id: customer.id } }">Edit</RouterLink>
                  </button>
                  <button type="button" class="mr-2 bg-blue-400 py-1 px-2 rounded">
                    <router-link :to="{ name: 'customers.view', params: { id: customer.id } }">View</router-link>
                  </button>
                  <button
                    type="button"
                    @click="deleteData(customer.id)"
                    class="bg-red-400 py-1 px-2 rounded"
                  >Delete</button>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </Layout>
</template> 
<script>
import Layout from '../../components/Layout.vue';
import { http } from '../../utils/http';
export default {
  components: {
    Layout,
  },
  data() {
    return {
      customers: [],
    }
  },
  methods: {
    getData() {
      http.get('/client/get/').then((response) => {
        this.customers = response.data;
        console.log('ooooooooooooooooooooooooooooooooooooooo');
      }).catch(error => {
        console.log(error);
      })
    },
    deleteData(id) {
      if (confirm('This element will be delete!!! ⚠⚠⚠')) {
        http.delete(`/client/${id}/delete/`).then(() => {
          this.getData()
        })
      }
    },
  },
  created: function () {
      this.getData()
    }
}

</script> 
