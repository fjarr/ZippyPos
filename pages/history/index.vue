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
                            Below is a list of completed purchase transactions. You can view the purchase details, items
                            bought, and the total price in the table below.
                        </p>

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
                                <tr>
                                    <td>1</td>
                                    <td>John Doe</td>
                                    <td>5</td>
                                    <td>Rp 500,000</td>
                                </tr>
                                <tr>
                                    <td>2</td>
                                    <td>Alice Smith</td>
                                    <td>3</td>
                                    <td>Rp 300,000</td>
                                </tr>
                            </tbody>
                        </table>

                        <div class="d-flex justify-content-between align-items-center mt-3 text-light">
                            <div>
                                <label for="pagination-select">Show:</label>
                                <select id="pagination-select" class="form-select text-light bg-transparent mt-3"
                                    style="width: 70px;">
                                    <option value="20" selected>20</option>
                                    <option value="50">50</option>
                                    <option value="100">100</option>
                                </select>
                            </div>

                            <nav>
                                <ul class="pagination">
                                    <li class="page-item"><a class="page-link text-light bg-transparent" href="#">«</a>
                                    </li>
                                    <li class="page-item"><a class="page-link text-light bg-transparent" href="#">1</a>
                                    </li>
                                    <li class="page-item"><a class="page-link text-light bg-transparent" href="#">2</a>
                                    </li>
                                    <li class="page-item"><a class="page-link text-light bg-transparent" href="#">3</a>
                                    </li>
                                    <li class="page-item"><a class="page-link text-light bg-transparent" href="#">»</a>
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
