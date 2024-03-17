<template>
  <div class="fooddetail">
    <navbar-component />
    <div class="container">
      <div class="row mt-5">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item "><router-link class="text-dark" to="/">Home</router-link></li>
              <li class="breadcrumb-item"><router-link class="text-dark" to="/foods">Foods</router-link></li>
              <li class="breadcrumb-item active" aria-current="page">Food Detail</li>
            </ol>
          </nav>
        </div>
      </div>
      <div class="row mt-4">
        <div class="col-md-6">
          <img :src="'../assets/images/' + product.gambar" class="img-fluid" alt="">
        </div>
        <div class="col-md-6">
          <h2><strong>{{ product.nama}}</strong></h2>
          <hr>
          <h4>Harga : Rp.{{product.harga}}</h4>
          <form action="" v-on:submit.prevent>
            <div class="form-group">
              <label for="jumlah_pemesanan" >Jumlah Pesan</label>
              <input type="number" class="form-control" v-model="pesan.jumlah_pesanan">
            </div>
            <div class="form-group">
              <label for="keterangan">Keterangan</label>
              <textarea
                  class="form-control"
                  placeholder="Keterangan: Pedas, Nasi Setengah .."
                  v-model="pesan.keterangan"
              ></textarea>
            </div>
            <button class="btn btn-success" @click="pemesanan"><b-icon-cart></b-icon-cart> Pesan</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import NavbarComponent from "@/components/NavbarComponent.vue";
import axios from "axios";

export default {
  name: 'FoodDetailView',
  components: {NavbarComponent},
  data() {
    return {
      product: {},
      pesan:{}
    }
  },
  methods: {
    setProduct(data) {
      this.product = data;
    },
    pemesanan() {
      this.pesan.product = this.product;
      if (this.pesan.jumlah_pesanan) {
        axios
            .post('http://localhost:4000/keranjangs', this.pesan)
            .then(() => {
              this.$router.push({path: '/keranjang'});
              this.$toast.success('sukses memasukan ke keranjang', {
                type: 'success',
                dismissible: true,
                duration: 3000
              })
            })
            .catch(() => {
              console.log('Gagal')
            })
      } else {
        this.$toast.warning('Jumlah pesanan tidak boleh kosong', {
          type: 'warning',
          dismissible: true,
          duration: 3000
        })
      }
    }

  },
  mounted() {
    axios
        .get('http://localhost:4000/products/'+ this.$route.params.id)
        .then((response) => {
          this.setProduct(response.data)
        })
        .catch((error) => { console.log(error) })
  }
}
</script>