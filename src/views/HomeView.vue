<template>
  <div class="home">
    <NavbarComponents />
    <div class="container">
      <Hero-components />
      <div class="row mt-4">
        <div class="col">
          <h2>Best <strong>Foods</strong></h2>
        </div>
        <div class="col">
          <router-link to="/foods" class="btn btn-success float-right">
            <b-icon-eye></b-icon-eye> Lihat Semua</router-link
          >
        </div>
      </div>

      <!-- card -->
      <div class="row mb-4">
        <!-- looping on vue -->
        <div
          class="col-md-4 mt-4"
          v-for="product in products"
          :key="product.id"
        >
          <CardProductComponent :product="product" />
        </div>
      </div>
      <!-- end-card -->
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import NavbarComponents from "../components/NavbarComponents.vue";
import HeroComponents from "../components/HeroComponents.vue";
import CardProductComponent from "../components/CardProductComponents.vue";
import axios from "axios";

export default {
  name: "HomeView",
  components: {
    NavbarComponents,
    HeroComponents,
    CardProductComponent,
  },
  data() {
    return {
      // Tangkap data menjadi onbject product
      products: [],
    };
  },

  methods: {
    // parameter data diambil dari backend
    setProducts(data) {
      // data tersebut menjadi product pada line 51
      this.products = data;
    },
  },
  // mounthed = Tempat coding bisa berjalan secara singkronus ataupun asingkronus
  mounted() {
    axios
      .get("http://localhost:3000/best-products")
      // mengisikan isi Api pada response pada setProduct
      .then((response) => this.setProducts(response.data))
      .catch((error) => console.log(error));
  },
};
</script>
