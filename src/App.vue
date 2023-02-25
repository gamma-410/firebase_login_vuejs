<template>
  <div id="app">

    <nav class="navbar navbar-light bg-light mb-5">
      <div class="container-fluid">
        <router-link class="navbar-brand" to="/">Firebase Login Study</router-link>
      </div>
    </nav>

    <div class="container">
      <router-view />
    </div>

  </div>
</template>

<style>
  a {
    text-decoration: none;
  }
</style>