<template>
  <div class="card shadow card-product">
    <img :src="'assets/images/'+ product.gambar " class="card-img-top" alt="...">
    <div class="card-body">
      <h5 class="card-title">{{product.nama}}</h5>
      <p>Harga: {{product.harga}}</p>
      <router-link :to="'foods/'+product.id" class="btn btn-success">Pesan</router-link>
    </div>
  </div>
</template>

<script >
export default {
  name: 'CartProduct',
  props: ['product']
}
</script>