<template>
  <header class="container-fluid pl-0 pr-0 border-bottom">
    <div class="d-flex m-3">
      <div class="col-6 d-flex justify-content-start">
        <h1 class=" mb-0">
          <nuxt-link class="text-warning text-decoration-none" to="/">
            [ Inside ]
          </nuxt-link>
        </h1>
      </div>
      <div class="col-6 d-flex justify-content-end">
        <a href="/login">
          <p class="text-warning pt-2 px-3">
            <i class="fas fa-arrow-left"></i>
          </p>
        </a>
        <p class="p-1 border border-warning rounded">
          <nuxt-link class="text-decoration-none text-warning" to="/dashboard">
            Menu
          </nuxt-link>
        </p>
      </div>
    </div>
  </header>
</template>
