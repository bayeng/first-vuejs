<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container">
      <a class="navbar-brand" href="#">Navbar</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item">
            <router-link class="nav-link" to="/">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/foods">
              Foods
            </router-link>
          </li>
        </ul>
        <ul class="navbar-nav ml-auto">
          <li class="nav-item">
            <router-link class="nav-link" to="/keranjang">
              Keranjang
              <b-icon-bag></b-icon-bag>
              <span class="badge badge-success ml-2">{{ jumlah_pesanan.length }}</span>
            </router-link>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
import axios from "axios";

export default {
  name: 'NavbarComponent',
  data() {
    return {
      jumlah_pesanan: []
    }
  },
  methods: {
    setJumlahPesanan(data) {
      this.jumlah_pesanan = data;
    }
  },
  mounted() {
    axios
        .get('http://localhost:4000/keranjangs')
        .then((response) => {
          this.setJumlahPesanan(response.data);
          console.log(this.jumlah_pesanan)
        })
        .catch((error) => {
          console.log(error)
        })
  }
}
</script>