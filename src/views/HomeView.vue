<template>
  <div class="home">
    <NavbarComponent />
    <div class="container">
      <HeroComponent/>

      <div class="row mt-4">
        <div class="col">
          <h1>Best Food</h1>
        </div>
        <div class="col">
          <router-link class="btn  btn-success float-right" to="/foods"><b-icon-eye></b-icon-eye> Lihat Semuanya</router-link>
        </div>
      </div>
      <div class="row mb-4">
        <div class="col-md-4 mt-3" v-for="product in products" :key="product.id">
          <CartProduct :product="product" />
        </div>
      </div>
    </div>
  </div>
</template>

<script >
// @ is an alias to /src
import NavbarComponent from "@/components/NavbarComponent.vue";
import HeroComponent from "@/components/HeroComponent.vue";
import CartProduct from "@/components/CardProduct.vue";
import axios from "axios";

export default {
  name: 'HomeView',
  components: {
    CartProduct,
    HeroComponent,
    NavbarComponent,
  },
  data() {
    return {
      products: []
    }
  },
  methods: {
    setProduct(data) {
      this.products = data;
    }
  },
  mounted() {
    axios
      .get('http://localhost:4000/best-products')
      .then((response) => {
        this.setProduct(response.data)
      })
        .catch((error) => {
          console.log(`gagal: ${error}`)
        })
  }
}
</script>
