<template>
    <div class="container-fluid">
        <div class="app d-flex">
            <div class="offcanvas offcanvas-start show rounded-4" tabindex="-1" id="offcanvasDark"
                aria-labelledby="offcanvasDarkLabel"
                style="background-color: darkslategrey; color: white; font-weight: 500; width: 20%; margin: 0.5%;">
                <div class="offcanvas-header">
                    <h2 class="offcanvas-title mb-4" id="offcanvasDarkLabel">ZippyPos</h2>
                    <br>
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
                                        <input type="text"
                                            class="form-control border-light bg-transparent text-light rounded-5"
                                            placeholder="Search..." style="font-size: 0.85rem; border-radius: 5px;">
                                        <span class="input-group-text bg-transparent border-0 text-light"
                                            style="border-radius: 0 5px 5px 0;">
                                            <i class="bi bi-search"></i>
                                        </span>
                                    </div>

                                </div>
                                <div class="row">
                                    <div v-for="(item, i) in menu" :key="i" class="col-3">
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
                                                            <button class="btn bg-transparent text-light mb-2">
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
                                    <div class="card p-2" style="background-color: rgb(40, 71, 71);">
                                        <div class="d-flex justify-content-between align-items-center">
                                            <div class="col-7">
                                                <p class="text-light mb-0" style="font-size: 0.8rem;">BASO IKAN</p>
                                            </div>
                                            <div class="d-flex align-items-center">
                                                <p class="text-light mb-0 me-3" style="font-size: 0.8rem;">3</p>
                                                <i class="bi bi-trash text-light" style="font-size: 0.8rem;"></i>
                                            </div>
                                        </div>
                                    </div>
                                    <div class="mt-auto">
                                        <div class="mt-3 border-top border-light pt-3">
                                            <div class="d-flex justify-content-between">
                                                <p class="text-light mb-0" style="font-size: 0.8rem;">Total Items</p>
                                                <p class="text-light mb-0" style="font-size: 0.8rem;">3</p>
                                            </div>
                                            <div class="d-flex justify-content-between">
                                                <p class="text-light mb-0" style="font-size: 0.8rem;">Total Price</p>
                                                <p class="text-light mb-0" style="font-size: 0.8rem;">Rp. 6,000,000</p>
                                            </div>
                                            <div class="mt-4 text-center">
                                                <button class="btn btn-light w-100"
                                                    style="font-size: 0.85rem;">Order</button>
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

const getmenu = async () => {
  const { data, error } = await supabase.from('menus').select('*')
  
  if (error) {
    console.error(error)
  }
  
  if (data) {
    menu.value = data
  }
}

onMounted(() => {
  getmenu()
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
