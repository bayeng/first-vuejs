<template>
  <div class="keranjang">
    <NavbarComponent />
    <div class="container">
      <div class="row mt-5">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item "><router-link class="text-dark" to="/">Home</router-link></li>
              <li class="breadcrumb-item"><router-link class="text-dark" to="/foods">Foods</router-link></li>
              <li class="breadcrumb-item active" aria-current="page">Keranjang</li>
            </ol>
          </nav>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <h2>Keranjang <strong>Saya</strong></h2>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <table class="table">
            <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">Foto</th>
              <th scope="col">Makanan</th>
              <th scope="col">Keterangan</th>
              <th scope="col">Jumlah</th>
              <th scope="col">Harga</th>
              <th scope="col">Total Harga</th>
              <th scope="col">Hapus</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="(keranjang, index) in keranjangs" :key="keranjang.id">
              <th scope="row">{{++index}}</th>
              <td>
                <img class="img-fluid" width="100pxpx" :src="'assets/images/'+keranjang.product.gambar" alt="">
              </td>
              <td>{{keranjang.product.nama}}</td>
              <td>{{keranjang.keterangan}}</td>
              <td>{{keranjang.jumlah_pesanan}}</td>
              <td>Rp.{{formatRupiah(keranjang.product.harga)}}</td>
              <td>Rp.{{formatRupiah(keranjang.jumlah_pesanan * keranjang.product.harga)}}</td>
              <td class="text-danger">
                <b-icon-trash></b-icon-trash>
              </td>
            </tr>
            <tr>
              <td colspan="6" align="right">Total: </td>
              <td>Rp.{{formatRupiah(totalHarga)}}</td>
            </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import NavbarComponent from "@/components/NavbarComponent.vue";
import axios from "axios";

export default {
  name: 'KeranjangView',
  components: {NavbarComponent},
  data() {
    return {
      keranjangs: [],
    }
  },
  methods: {
    setKeranjangs(data) {
      this.keranjangs = data
    },

  },
  mounted() {
    axios
        .get('http://localhost:4000/keranjangs')
        .then((response) => {
          const data = response.data;
          this.setKeranjangs(data)
         });
  },
  computed: {
    totalHarga() {
      return this.keranjangs.reduce((items, data) => {
        return items+(data.jumlah_pesanan * data.product.harga)
      }, 0)
    },
    formatRupiah() {
      return (angka) => {
        return angka.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".");
      };
    }
  }
}
</script>