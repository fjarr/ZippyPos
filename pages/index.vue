<template>
    <div class="container-fluid">
      <div class="app d-flex">
          <div class="offcanvas offcanvas-start show rounded-4" tabindex="-1" id="offcanvasDark"
              aria-labelledby="offcanvasDarkLabel">
              <div class="offcanvas-header">
                  <h2 class="offcanvas-title mb-2" id="offcanvasDarkLabel">ZippyPos <img src="../assets/img/ZIPPYw.png" style="width:20%;"> </h2>
                  <br>
              </div>
              <div class="offcanvas-body">
                  <ul class="navbar-nav mb5">
                      <li class="nav-item mb-3">
                          <span class="nav-link-text ms-1"> <div class="card p-2">Dashboard</div></span>
                      </li>
                      <li class="nav-item mb-3">
                        <nuxt-link to="../cashier" class="text-decoration-none text-white ms-1">
                          <span class="nav-link-text">cashier</span>
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
          <div class="content-wrapper">
              <div class="card mb-3 mx-auto">
                  <nuxt-link to="mailto:fjarr47@gmail.com?subject=Subjek%20Pesan" class="text-decoration-none text-white">
                  <div class="card-body">
                          <h6 style="text-align: center;">Do You Need Help? <i
                                  class="bi bi-envelope-at-fill mx-4"></i></h6>
                  </div>
                  </nuxt-link>
              </div>
              <div class="card">
                  <div class="card-body">
                      <h3>Dashboard</h3>
                      <p>Check sales results, income today, this month and this year, as well as today's buyers.</p>
                      <div class="row">
                          <div class="col-4 mb-3">
                              <div class="card">
                                  <div class="card-body">
                                      <blockquote class="blockquote mb-0">
                                          <p>Number of Buyers Today</p>
                                          <footer class="blockquote-footer">12:ORG</footer>
                                      </blockquote>
                                  </div>
                              </div>
                          </div>
                          <div class="col-4  mb-3">
                              <div class="card">
                                  <div class="card-body">
                                      <blockquote class="blockquote mb-0">
                                          <p>Today's Income</p>
                                          <footer class="blockquote-footer">RP:20000</footer>
                                      </blockquote>
                                  </div>
                              </div>
                          </div>
                          <div class="col-4  mb-3">
                              <div class="card">
                                  <div class="card-body">
                                      <blockquote class="blockquote mb-0">
                                          <p>income this month</p>
                                          <footer class="blockquote-footer">RP: 100000</footer>
                                      </blockquote>
                                  </div>
                              </div>
                          </div>
                          <div class="col-4 mb-3">
                              <div class="card">
                                  <div class="card-body">
                                      <blockquote class="blockquote mb-0">
                                          <p>This Year's Revenue</p>
                                          <footer class="blockquote-footer">RP: 20000000 </footer>
                                      </blockquote>
                                  </div>
                              </div>
                          </div>
                          <div class="col-4 mb-3">
                              <div class="card">
                                  <div class="card-body">
                                      <blockquote class="blockquote mb-0">
                                          <p>items purchased today</p>
                                          <footer class="blockquote-footer">12 :Items </footer>
                                      </blockquote>
                                  </div>
                              </div>
                          </div>
                          <div class="col-4 mb-3">
                              <div class="card">
                                  <div class="card-body">
                                      <blockquote class="blockquote mb-0">
                                          <p>View All Income</p>
                                          <footer class="blockquote-footer">All Purchase History </footer>
                                      </blockquote>
                                  </div>
                              </div>
                          </div>
                          <div class="col-4">
                              <div class="card">
                                  <div class="card-body">
                                      <blockquote class="blockquote mb-0">
                                          <p>History Today</p>
                                      </blockquote>
                                      <table class="table text-light">
                                          <thead>
                                              <tr>
                                                  <th scope="col">NO</th>
                                                  <th scope="col">Items</th>
                                                  <th scope="col">Price</th>
                                              </tr>
                                          </thead>
                                          <tbody>
                                              <tr>
                                                  <th scope="row">1</th>
                                                  <td>12 items</td>
                                                  <td>20000</td>
                                              </tr>
                                              <tr>
                                                  <th scope="row">2</th>
                                                  <td>4 items</td>
                                                  <td>10000</td>
                                              </tr>
                                          </tbody>
                                      </table>
                                  </div>
                              </div>
                          </div>
                          <div class="col-8">
                              <div class="card">
                                  <div class="card-body">
                                      <blockquote class="blockquote mb-0">
                                          <p>Statistics</p>
                                      </blockquote>
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

<style scoped>
@import url("https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css");

 .container-fluid{
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
  background-color: darkslategrey;
  color: white;
  font-weight: 500;
  width: 20%;
  margin: 0.5%;
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

.card.mb-3.mx-auto {
  width: 50%;
}

.card h6 {
  text-align: center;
}

.card table thead th {
  color: lightgray;
}
</style>
