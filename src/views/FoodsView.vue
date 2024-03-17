<template>
  <div class="foods">
    <NavbarComponent />
    <div class="container">
      <div class="row mt-4">
        <div class="col">
          <h1>Daftar <strong>Makanan</strong></h1>
        </div>
      </div>
      <div class="row mb-4">
        <div class="col-md-4 mb-4" v-for="product in products" :key="product.id">
          <CartProduct :product="product" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import NavbarComponent from "@/components/NavbarComponent.vue";
  import CartProduct from "@/components/CardProduct.vue";
  import axios from "axios";

  export default {
    name: "FoodsView",
    components: {CartProduct, NavbarComponent},
    data() {
      return {
        products: []
      }
    },
    methods: {
      setProduct(data) {
        this.products = data;
      },
    },
    mounted() {
      axios
          .get('http://localhost:4000/products')
          .then((response) => {
            console.log(response)
            this.setProduct(response.data)
          })
          .catch((error) => {
            console.log(error)
          })
    }
  }
</script>