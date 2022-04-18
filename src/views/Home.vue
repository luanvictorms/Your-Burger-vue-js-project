<template>
  <Banner />
  <div class="container-form">
    <div class="main-container">
      <h1>Monte o seu Burguer:</h1>
      <BurguerForm />
    </div>
  </div>
</template>

<script>
import Banner from "../components/Banner.vue";
import BurguerForm from "../components/BurguerForm.vue";

export default {
  name: "Home",
  components: {
    Banner,
    BurguerForm
  },
}
</script>
