<template>
    <div class="container-fluid bg-image">
      <div class="row justify-content-center align-items-center">
        <div class="col-md-3 col-sm-5">
          <div class="card   rounded-5 bg-dark border-2 border-white">
            <form @submit.prevent="Login">
              <div class="card-title mt-4 mb-4">
              </div>
              <div class="mb-4 px-5">
                <input v-model="email" type="email" class="form-control rounded-5" placeholder="Email ......." />
              </div>
              <div class="mb-4 px-5">
                <input v-model="password" type="password" class="form-control rounded-5" placeholder="Password ......." />
              </div>
              <button type="submit" class="btn btn-light rounded-5" >LOGIN</button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  const supabase = useSupabaseClient();
  const email = ref('');
  const password = ref('');
  
  const Login = async () => {
    const { data, error } = await supabase.auth.signInWithPassword({
      email: email.value,
      password: password.value,
    });
  
    if (error) {
      alert('Password atau email Anda salah');
    } else {
      navigateTo('/');
    }
  };
  
  </script>