<template>
    <div class="container-fluid">
      <div class="app d-flex">
        <div class="offcanvas offcanvas-start show rounded-4" tabindex="-1" id="offcanvasDark"
          aria-labelledby="offcanvasDarkLabel"
          style="background-color: darkslategrey; color: white; font-weight: 500; width: 20%; margin: 0.5%;">
          <div class="offcanvas-header">
            <h2 class="offcanvas-title mb-3" id="offcanvasDarkLabel">ZippyPos <img src="../../assets/img/ZIPPYw.png" style="width:20%;"> </h2>            <br>
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
                  <span class="nav-link-text">cashier</span>
                </nuxt-link>
              </li>
              <li class="nav-item mb-3">
                <nuxt-link to="../inputmenu" class="text-decoration-none text-white ms-1">
                  <span class="nav-link-text"><div class="card p-2">Input Menu</div></span>
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
          <div class="card">
            <div class="card-body">
              <h3 class="mt-4 mx-5">Input Menu</h3>
              <p class="mx-5">Add the menu you want, adjust the menu to your company, here you add the menu name and menu price.</p>
              <div class="row d-flex justify-content-center m-3">
                <div class="col-8 py-2 px-5">
                  <div class="card px-5 py-5">
                    <h4 class="d-flex justify-content-center mb-2 mt-2">Input Here</h4>
                    <form @submit.prevent="Imenu" class="px-5 py-5">
                      <div class="mb-4">
                        <label class="form-label">MENU NAME</label>
                        <input v-model="name" type="text" class="form-control border-light text-light bg-transparent">
                      </div>
                      <div class="mb-3">
                        <div class="mb-4">
                          <label class="form-label">PRICE</label>
                          <input v-model="price" type="text" class="form-control border-light text-light bg-transparent">
                        </div>
                      </div>
                      <button type="submit" class="btn border-light text-light" style="background-color: rgb(40, 71, 71)">Submit</button>
                    </form>
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
    const supabase = useSupabaseClient();
    const name = ref('');
    const price = ref('');
  
    const Imenu = async () => {
      const { error } = await supabase.from('menus').insert([
        { name: name.value, price: price.value }
      ]);
      if (!error) {
        navigateTo('../datamenu');
      } else {
        console.error('Error inserting data:', error);
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
</style>
