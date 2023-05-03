<template>
  <div>
    <NavbarComponents />
    <div class="container">
      <div class="row mt-4">
        <div class="col">
          <h2>Daftar <strong>makanan</strong></h2>
        </div>
      </div>
      <!-- input  -->
      <div class="row mt-3">
        <div class="col">
          <div class="input-group mb-3">
            <!-- penamaan v-model haris sama dengan return data yang dituju(search) -->
            <input
              v-model="search"
              type="text"
              class="form-control"
              placeholder="Cari Makanan kesukaan anda .."
              aria-label="Cari"
              aria-describedby="basic-addon1"
              @keyup="searchFood"
            />
            <div class="input-group-prepend">
              <span class="input-group-text" id="basic-addon1"
                ><b-icon-search></b-icon-search
              ></span>
            </div>
          </div>
        </div>
      </div>
      <!-- end-input  -->
      <div class="row mb-3">
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
      </div>
    </div>
  </div>
</template>

<script>
import NavbarComponents from "../components/NavbarComponents.vue";
import CardProductComponent from "../components/CardProductComponents.vue";
import axios from "axios";

export default {
  name: "FoodsView",
  components: {
    NavbarComponents,
    CardProductComponent,
  },
  data() {
    return {
      products: [],
      search: "",
    };
  },

  methods: {
    // parameter data diambil dari backend
    setProducts(data) {
      // data tersebut menjadi product pada line 51
      this.products = data;
    },
    searchFood() {
      axios
        .get("http://localhost:3000/products?q=" + this.search)
        // mengisikan isi Api pada response pada setProduct
        .then((response) => this.setProducts(response.data))
        .catch((error) => console.log(error));
    },
  },
  // mounthed = Tempat coding bisa berjalan secara singkronus ataupun asingkronus
  mounted() {
    axios
      .get("http://localhost:3000/products")
      // mengisikan isi Api pada response pada setProduct
      .then((response) => this.setProducts(response.data))
      .catch((error) => console.log(error));
  },
};
</script>

<style></style>
