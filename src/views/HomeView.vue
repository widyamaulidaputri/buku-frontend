<template>
  <!--banner image-->

  <div class="banner-image w-100 vh-100 d-flex justify-content-center align-items-center">
    <div class="content text-center">
      <h1 class="text-white">Welcome To My Library </h1>
      <h2 class="text-start">Start Here, Go AnyWhere</h2>
    </div>
    <div class = "col-lg-6">
      <img src="../assets/perpus.jpg" class="img-fluid">
    </div>
  </div>

</template>

<script>
export default {
  name: 'App',
  components: {
    // HelloWorld
  }
}
</script>

<style>
.banner-image{
  background: rgb(59, 167, 123);
  font-family: "Source Sans Pro" ;
  font-style: italic;
  font-size: 30px;

}

</style>