<template>
  <div class="container-fluid">
    <div class="app d-flex">
      <div class="offcanvas offcanvas-start show rounded-4" tabindex="-1" id="offcanvasDark"
        aria-labelledby="offcanvasDarkLabel"
        style="background-color: darkslategrey; color: white; font-weight: 500; width: 20%; margin: 0.5%;">
        <div class="offcanvas-header">
          <h2 class="offcanvas-title mb-4" id="offcanvasDarkLabel">ZippyPos</h2>
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
                <span class="nav-link-text">
                  <div class="card p-2">Menu Data</div>
                </span>
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
        <div class="card">
          <div class="card-body p-5">
            <h3 class="mb-3 text-light">Data Menu</h3>
            <p class="text-light mb-5" style="font-size: 0.9rem;">Manage and view the menu items, including their names
              and prices. You can edit or delete items as needed.</p>
            <table class="table text-light">
              <thead>
                <tr>
                  <th scope="col">No</th>
                  <th scope="col">Name Menu</th>
                  <th scope="col">Price</th>
                  <th scope="col">Action</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(item, i) in menu" :key="item.id">
                  <th scope="row">{{ i + 1 }}</th>
                  <td>{{ item.name }}</td>
                  <td>{{ item.price }}</td>
                  <td>
                    <button class="btn text-light" style="font-size: 0.85rem;" @click="deleteMenu(item.id)">
                      <i class="bi bi-trash"></i>
                    </button>
                  </td>
                </tr>
              </tbody>
            </table>
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

const deleteMenu = async (id) => {
  const { error } = await supabase.from('menus').delete().eq('id', id)
  
  if (error) {
    console.error("Error deleting menu item:", error)
  } else {
    getmenu()
  }
}

onMounted(() => {
  getmenu()
})
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
</style>
