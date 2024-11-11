<template>
    <div class="container-fluid">
      <div class="app d-flex">
        <div class="offcanvas offcanvas-start show rounded-4" tabindex="-1" id="offcanvasDark" aria-labelledby="offcanvasDarkLabel" style="background-color: darkslategrey; color: white; font-weight: 500; width: 20%; margin: 0.5%;">
          <div class="offcanvas-header">
            <h2 class="offcanvas-title mb-3" id="offcanvasDarkLabel">ZippyPos <img src="../../assets/img/ZIPPYw.png" style="width:20%;"> </h2><br>
          </div>
          <div class="offcanvas-body">
            <ul class="navbar-nav mb5">
              <li class="nav-item mb-3">
                <nuxt-link to="../" class="text-decoration-none text-white ms-1">
                  <span class="nav-link-text ms-1"> Dashboard</span>
                </nuxt-link>
              </li>
              <li class="nav-item mb-3">
                <nuxt-link to="../cashier" class="text-decoration-none text-white ms-1">
                  <span class="nav-link-text">Cashier</span>
                </nuxt-link>
              </li>
              <li class="nav-item mb-3">
                <nuxt-link to="../inputmenu" class="text-decoration-none text-white ms-1">
                  <span class="nav-link-text">Input Menu</span>
                </nuxt-link>
              </li>
              <li class="nav-item mb-3">
                <nuxt-link to="../datamenu" class="text-decoration-none text-white ms-1">
                  <span class="nav-link-text">Menu Data</span>
                </nuxt-link>
              </li>
              <li class="nav-item mb-3">
                <nuxt-link to="../history" class="text-decoration-none text-white ms-1">
                  <span class="nav-link-text">
                    <div class="card p-2">Transaction History</div>
                  </span>
                </nuxt-link>
              </li>
            </ul>
            <h5 class="mt-5">Sign out</h5>
          </div>
        </div>
  
        <div class="content-wrapper mt-2">
          <div class="card p-5">
            <div class="card-body">
              <h4 class="card-title">Transaction History</h4>
              <p class="card-text mb-5">
                Below is a list of completed purchase transactions. You can view the purchase details, items bought, and the total price in the table below.
              </p>
  
              <div class="d-flex justify-content-between align-items-center mb-4">
                <div>
                  <label for="pagination-select">Show:</label>
                  <select id="pagination-select" v-model="perPage" class="form-select text-light bg-transparent mt-3" style="width: 70px;">
                    <option class=" text-dark " value="10">10</option>
                    <option class=" text-dark" value="20">20</option>
                    <option class=" text-dark " value="50">50</option>
                  </select>
                </div>
              </div>
              <table class="table text-light">
                <thead>
                  <tr>
                    <th>No</th>
                    <th>Buyer Name</th>
                    <th>Total Items</th>
                    <th>Total Price</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="(buyer, i) in filteredBuyers.slice(startIndex, endIndex)" :key="buyer.id">
                    <td>{{ startIndex + i + 1 }}</td>
                    <td>{{ buyer.pelanggan }}</td>
                    <td>{{ buyer.items }}</td>
                    <td>{{ buyer.jumlah }}</td>
                  </tr>
                </tbody>
              </table>
  
              <div class="d-flex justify-content-between align-items-center mt-3 text-light">
                <nav>
                  <ul class="pagination">
                    <li class="page-item" :class="{ disabled: currentPage === 1 }">
                      <a class="page-link text-light bg-transparent" href="#" @click.prevent="goToPage(currentPage - 1)">«</a>
                    </li>
                    <li v-for="page in totalPages" :key="page" class="page-item" :class="{ active: currentPage === page }">
                      <a class="page-link text-light bg-transparent" href="#" @click.prevent="goToPage(page)">{{ page }}</a>
                    </li>
                    <li class="page-item" :class="{ disabled: currentPage === totalPages }">
                      <a class="page-link text-light bg-transparent" href="#" @click.prevent="goToPage(currentPage + 1)">»</a>
                    </li>
                  </ul>
                </nav>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted, computed } from 'vue';
  const supabase = useSupabaseClient();
  
  const buyers = ref([]);
  const perPage = ref(10);
  const currentPage = ref(1);
  
  const getbuyer = async () => {
    const { data, error } = await supabase.from('transactions').select('*');
    if (error) {
      console.error(error);
    }
    if (data) {
      buyers.value = data;
    }
  };
  
  onMounted(() => {
    getbuyer();
  });
  
  const filteredBuyers = computed(() => {
    return buyers.value;
  });
  
  const startIndex = computed(() => (currentPage.value - 1) * perPage.value);
  const endIndex = computed(() => currentPage.value * perPage.value);
  
  const totalPages = computed(() => Math.ceil(filteredBuyers.value.length / perPage.value));
  
  const goToPage = (page) => {
    if (page >= 1 && page <= totalPages.value) {
      currentPage.value = page;
    }
  };
  
  </script>
  
  <style scoped>
  @import url("https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css");
  
  .container-fluid {
    background-color: rgb(40, 71, 71);
    margin: 0;
  }
  
  .app {
    display: flex;
    height: 100vh;
  }
  
  .offcanvas {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    z-index: 1045;
    transition: transform 0.3s ease;
  }
  
  .content-wrapper {
    margin-left: 22%;
    width: 80%;
    margin-right: 1%;
  }
  
  .card {
    background-color: darkslategrey;
    color: white;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  }
  
  .card-body {
    padding: 20px;
  }
  
  .pagination {
    display: flex;
    gap: 5px;
  }
  </style>
  