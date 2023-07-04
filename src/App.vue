<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-success">
      <div class="container">
        <router-link to="/" class="navbar-brand text-white">MY LIBRARIES</router-link>
        <ul class="navbar-nav ml-auto">
          <li class="nav-item">
            <router-link to="/books" class="nav-link text-white">Book Store</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/categories" class="nav-link text-white">Categories</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/Member" class="nav-link text-white">Member</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/desc" class="nav-link text-white">Description</router-link>
          </li><li class="nav-item">
        </li>
        </ul>
      </div>
    </nav>
    <div class="container mt-4">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
};
</script>

<style>

#app {

  font-family: Arial, Helvetica sans-serif;
}
.navbar-expand-lg {
  background-color: #78CEA9FF;
}
.navbar-brand{
  padding: 5px 10px;
  text-decoration: none;
  color: white;
  font-family: "Source Sans Pro";
  font-size: large;
}
.navbar-nav li:hover {
  color: #06060b;
  font-size: 20px;
  transition: .2s;
  background-color:  #78CEA9FF;
}
</style>
