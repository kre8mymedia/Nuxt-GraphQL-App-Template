<template>
  <nav id="myNav" class="navbar navbar-expand-lg bg-dark navbar-dark">
    <a class="navbar-brand" href="/">GraphQL Laravel</a>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>

    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav mr-auto">
        <li class="nav-item active">
          <a class="nav-link" href="/">Home <span class="sr-only">(current)</span></a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="/about">About</a>
        </li>
        
        <!-- <li class="nav-item">
          <a class="nav-link disabled" href="#" tabindex="-1" aria-disabled="true">Disabled</a>
        </li> -->
      </ul>
      <ul v-if="isLoggedIn == false" class="navbar-nav ml-auto">
        <li class="nav-item">
          <a href="/login" class="nav-link">Login</a>
        </li>
        <li class="nav-item">
          <a class="nav-link" href="/register">Register</a>
        </li>
      </ul>
      <ul v-else class="navbar-nav ml-auto">
        <li style="border-radius: 3px;" class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
            ryan.eggleston@tmgcore.com
          </a>
          <div class="dropdown-menu" aria-labelledby="navbarDropdown">
            <a class="dropdown-item" href="/account">Account</a>
            <a class="dropdown-item" href="/records">Records</a>
            <div class="dropdown-divider"></div>
            <a v-on:click="toggleLogin" class="dropdown-item">Logout</a>
          </div>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      isLoggedIn: true
    }
  },
  methods: {
    toggleLogin: function() {
      this.isLoggedIn = false
    }
  }

}
</script>

<style>
  #myNav {
    background: #00c6ff; /* fallback for old browsers */
    background: -webkit-linear-gradient(to right, #00c6ff, #0072ff); /* Chrome 10-25, Safari 5.1-6 */
    background: linear-gradient(to right, #00c6ff, #0072ff); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  }
</style>