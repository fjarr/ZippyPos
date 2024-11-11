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
                  <span class="nav-link-text"><div class="card p-2">cashier</div></span>
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
                  <span class="nav-link-text">Transaction History</span>
                </nuxt-link>
              </li>
            </ul>
            <h5 class="mt-5">Sign out</h5>
          </div>
        </div>
  
        <div class="content-wrapper mt-2">
          <div class="card" style="height: 97vh">
            <div class="card-body">
              <div class="row">
                <div class="col-9">
                  <div class="col-12 mb-3">
                    <div class="input-group">
                      <input type="text" v-model="searchQuery" class="form-control border-light bg-transparent text-light rounded-5" placeholder="Search..." style="font-size: 0.85rem; border-radius: 5px;">
                      <span class="input-group-text bg-transparent border-0 text-light" style="border-radius: 0 5px 5px 0;">
                        <i class="bi bi-search"></i>
                      </span>
                    </div>
                  </div>
                  <div class="row">
                    <div v-for="(item, i) in filteredMenu" :key="i" class="col-3">
                      <div class="card m">
                        <div class="row pe-4">
                          <div class="col-1">
                            <div class="card bg-light" style="height: 100%;"></div>
                          </div>
                          <div class="col-10">
                            <h6 class="mb-5 mt-2">{{ item.name }}</h6>
                            <div class="row pb-2">
                              <div class="col-9 pt-2">
                                {{ item.price }}
                              </div>
                              <div class="col-3">
                                <button class="btn bg-transparent text-light mb-2" @click="addItemToOrder(item)">
                                  <i class="bi bi-cart-plus-fill"></i>
                                </button>
                              </div>
                            </div>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
  
                <div class="col-3">
                  <div class="card p-2" style="height: 91vh; font-size: 0.85rem;">
                    <div v-for="(item, index) in selectedItems" :key="index" class="card p-2 mb-2" style="background-color: rgb(40, 71, 71);">
                      <div class="d-flex justify-content-between align-items-center">
                        <div class="col-7">
                          <p class="text-light mb-0" style="font-size: 0.8rem;">{{ item.name }}</p>
                        </div>
                        <div class="d-flex align-items-center">
                          <p class="text-light mb-0 me-3" style="font-size: 0.8rem;">{{ item.quantity }}</p>
                          <i class="bi bi-trash text-light" style="font-size: 0.8rem;" @click="removeItemFromOrder(index)"></i>
                        </div>
                      </div>
                    </div>
  
                    <div class="mt-auto">
                      <div class="mt-3 border-top border-light pt-3">
                        <div class="d-flex justify-content-between mb-2">
                          <p class="text-light mb-0" style="font-size: 0.8rem;">Name</p>
                          <p class="text-light mb-0" style="font-size: 0.8rem;">
                            <input type="text" v-model="customerName" placeholder="Enter Name">
                          </p>
                        </div>
                        <div class="d-flex justify-content-between mb-2">
                          <p class="text-light mb-0" style="font-size: 0.8rem;">Total Items</p>
                          <p class="text-light mb-0" style="font-size: 0.8rem;">{{ totalItems }}</p>
                        </div>
                        <div class="d-flex justify-content-between mb-2">
                          <p class="text-light mb-0" style="font-size: 0.8rem;">Total Price</p>
                          <p class="text-light mb-0" style="font-size: 0.8rem;">Rp. {{ totalPrice }}</p>
                        </div>
                        <div class="d-flex justify-content-between mb-2">
                          <p class="text-light mb-0" style="font-size: 0.8rem;">Discount (%)</p>
                          <p class="text-light mb-0" style="font-size: 0.8rem;">
                            <input type="number" v-model="discount" placeholder="Enter Discount">
                          </p>
                        </div>
                        <div class="d-flex justify-content-between mb-2">
                          <p class="text-light mb-0" style="font-size: 0.8rem;">Payment Amount</p>
                          <p class="text-light mb-0" style="font-size: 0.8rem;">Rp. {{ paymentAmount }}</p>
                        </div>
                        <div class="mt-4 text-center">
                          <button class="btn btn-light w-100" @click="placeOrder" style="font-size: 0.85rem;">Order</button>
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  const supabase = useSupabaseClient()
  
  const menu = ref([])
  const customerName = ref('')
  const selectedItems = ref([])
  const searchQuery = ref('')
  const discount = ref(0)
  
  const getMenu = async () => {
    const { data, error } = await supabase.from('menus').select('*')
    if (error) {
      console.error(error)
    }
    if (data) {
      menu.value = data
    }
  }
  
  onMounted(() => {
    getMenu()
  })
  
  const addItemToOrder = (item) => {
    const existingItem = selectedItems.value.find(i => i.id === item.id)
    if (existingItem) {
      existingItem.quantity++
    } else {
      selectedItems.value.push({ ...item, quantity: 1 })
    }
  }
  
  const removeItemFromOrder = (index) => {
    selectedItems.value.splice(index, 1)
  }
  
  const totalPrice = computed(() => {
    return selectedItems.value.reduce((total, item) => total + item.price * item.quantity, 0)
  })
  
  const totalItems = computed(() => {
    return selectedItems.value.reduce((total, item) => total + item.quantity, 0)
  })
  
  const paymentAmount = computed(() => {
    const discountAmount = (discount.value / 100) * totalPrice.value
    return totalPrice.value - discountAmount
  })
  
  const placeOrder = async () => {
    if (!customerName.value.trim() || selectedItems.value.length === 0) {
      alert("Please enter customer name and select items.")
      return
    }
  
    const { data, error } = await supabase.from('transactions').insert([
      {
        jumlah: paymentAmount.value,
        pelanggan: customerName.value,
        items: selectedItems.value.length,
      }
    ])
  
    if (error) {
      console.error(error)
      alert("Failed to place order.")
    } else {
      alert("Order placed successfully!")
      selectedItems.value = []
      customerName.value = ''
      discount.value = 0
    }
  }
  
  const filteredMenu = computed(() => {
    return menu.value.filter(item =>
      item.name.toLowerCase().includes(searchQuery.value.toLowerCase())
    )
  })
  </script>
  
  <style scoped>
  @import url("https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css");
  
  .card.m {
    background-color: rgb(40, 71, 71);
  }
  
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
  </style>
  