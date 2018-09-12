<template>
  <div id="app">
    <div class="container-fluid">

      <div class="row">
        <div class="col-lg jumbotron jumbotron-fluid bg-success">
          <div class="clearfix m-y-25">
            <!-- jika sudah login -->
            <button v-if="hasLogin" :class="isLogin" class="btn tombol rounded-circle float-right m-x-5 shadow-lg rounded" @click="logout()"><a class="text-muted" >{{statusLogin}}</a></button>
            <!-- jika belum login -->
            <button v-if="!hasLogin" :class="isLogin" class="btn tombol rounded-circle float-right m-x-5 shadow-lg rounded" data-toggle="modal" data-target="#loginModal"><a class="text-muted" >{{statusLogin}}</a></button>

            <button class="btn btn-secondary tombol rounded-circle float-right m-x-10 shadow-lg bg-white rounded" @click="about()"><a class="text-muted">Bantuan</a></button>
          </div>
          <h1 class="text-center text-white display-4">Seller Recommendation</h1>
          <p class="text-center lead text-muted">help you to looking for some goods with the best recommentadion</p>
        </div>

        <div id="loginModal" class="modal fade" role="dialog">
          <div class="modal-dialog">
            <!-- konten modal-->
            <div class="modal-content">
              <!-- heading modal -->
              <div class="modal-header">
                <button type="button" class="close" data-dismiss="modal">&times;</button>
                  <h4 class="modal-title">Login</h4>
              </div>
              <!-- body modal -->
              <div class="modal-body container-fluid">
                <form class="form-group">
                  <input class="form-control" ref="username" placeholder="Username">
                  <br>
                  <input type="password" class="form-control" ref="password" placeholder="Password">
                </form>
                <a class="link" data-dismiss="modal" data-toggle="modal" data-target="#registrasiModal">Registrasi</a> |
                <a class="link" data-dismiss="modal" data-toggle="modal" data-target="#lostPasswordModal">Lupa Password ?</a>
              </div>
              <!-- footer modal -->
              <div class="modal-footer">
                <button @click="login()" data-dismiss="modal" type="button" class="btn btn-default">Login</button>
              </div>
            </div>
          </div>
        </div>

        <div id="registrasiModal" class="modal fade" role="dialog">
          <div class="modal-dialog">
            <!-- konten modal-->
            <div class="modal-content">
              <!-- heading modal -->
              <div class="modal-header">
                <button type="button" class="close" data-dismiss="modal">&times;</button>
                  <h4 class="modal-title">Registrasi</h4>
              </div>
              <!-- body modal -->
              <div class="modal-body container-fluid">
                <form class="form-group">
                  <input type="email" class="form-control" ref="usernameReg" placeholder="Email" @keydown.enter.prevent="registrasi()">
                  <br>
                  <input class="form-control" ref="displayNameReg" placeholder="Display Name" @keydown.enter.prevent="registrasi()">
                  <br>
                  <input type="password" class="form-control" ref="passwordReg" placeholder="Password" @keydown.enter.prevent="registrasi()">
                </form>
              </div>
              <!-- footer modal -->
              <div class="modal-footer">
                <button @click="registrasi()" data-dismiss="modal" type="button" class="btn btn-default">Daftar</button>
              </div>
            </div>
          </div>
        </div>

        <div id="lostPasswordModal" class="modal fade" role="dialog">
          <div class="modal-dialog">
            <!-- konten modal-->
            <div class="modal-content">
              <!-- heading modal -->
              <div class="modal-header">
                <button type="button" class="close" data-dismiss="modal">&times;</button>
                  <h4 class="modal-title">Lost Password</h4>
              </div>
              <!-- body modal -->
              <div class="modal-body container-fluid">
                <form class="form-group">
                  <input type="email" class="form-control container" @keydown.enter.prevent="lupaPassword()" ref="emailLostPassword" placeholder="Masukan email anda !">
                </form>
              </div>
              <!-- footer modal -->
              <div class="modal-footer">
                <button @click="lupaPassword()" data-dismiss="modal" type="button" class="btn btn-default">Send</button>
              </div>
            </div>
          </div>
        </div>

      </div>
      <div class="row">
        <div class="col-lg-2">
          <div class="container">
            <h1>Hello,</h1>
            <h2 class="text-muted">{{displayName}}</h2>
          </div>
          <div class="container py-3">
            <p class="h5">Pilih Online Shop :</p>
            <br>
            <div class="form-check">
              <label class="form-check-label">
                <input class="form-check-input" name="toko" v-model="toko" type="radio" value="tokopedia" checked> Tokopedia
              </label>
            </div>
            <div class="form-check">
              <label class="form-check-label">
                <input class="form-check-input" name="toko" v-model="toko" type="radio" value="bukalapak"> Bukalapak
              </label>
            </div>
            <div class="form-check">
              <label class="form-check-label">
                <input class="form-check-input" name="toko" v-model="toko" type="radio" value="shopee"> Shopee
              </label>
            </div>
          </div>
        </div>
        <div class="col-lg-10">
          <div class="row container">
           <div class="col-lg-12">
            <h3 class="titled" align="left">Masukkan Ranking berdasar Prioritas : </h3>
            <p class="text-muted" style="font-size: 4 !important;" >1: Paling Penting -> 5: Paling tidak Penting</p>
           </div>
           <div class="col-lg-12">
            <form class="form-inline">
              <select v-model="price" class="form-control form-control-sm col-lg-1">
                <option selected value=""></option>
                <option value="1">1</option>
                <option value="2">2</option>
                <option value="3">3</option>
                <option value="4">4</option>
                <option value="5">5</option>
              </select> &nbsp;Harga&nbsp;

              <select v-model="sellerLocation" class="form-control form-control-sm col-lg-1">
                <option selected value=""></option>
                <option value="1">1</option>
                <option value="2">2</option>
                <option value="3">3</option>
                <option value="4">4</option>
                <option value="5">5</option>
              </select> &nbsp;Lokasi Seller&nbsp;

              <select v-model="sellerRating" class="form-control form-control-sm col-lg-1">
                <option selected value=""></option>
                <option value="1">1</option>
                <option value="2">2</option>
                <option value="3">3</option>
                <option value="4">4</option>
                <option value="5">5</option>
              </select> &nbsp;Reputasi&nbsp;

              <select v-model="numProductSold" class="form-control form-control-sm col-lg-1">
                <option selected value=""></option>
                <option value="1">1</option>
                <option value="2">2</option>
                <option value="3">3</option>
                <option value="4">4</option>
                <option value="5">5</option>
              </select> &nbsp;Jumlah Produk Terjual&nbsp;

              <select v-model="expedition" class="form-control form-control-sm col-lg-1">
                <option selected value=""></option>
                <option value="1">1</option>
                <option value="2">2</option>
                <option value="3">3</option>
                <option value="4">4</option>
                <option value="5">5</option>
              </select> &nbsp;Dukungan Ekspedisi&nbsp;
            </form>
           </div>
           <div class="col-lg-12 py-3">
            <form class="form-inline">
              <input class="form-control col-lg-5 mb-2 mr-sm-2 mb-sm-0" placeholder="Mau belanja apa ?" ref="item" v-model="item" required>
              <input class="form-control col-lg-2" placeholder="Lokasi / Area" ref="currentLocation" v-model="pilih" data-toggle="modal" data-target="#myModal" readonly required> &nbsp;
              <button @click.prevent="search()" type="submit" class="btn btn-success">Cari !</button>
              
              <!-- modal -->
              <div id="myModal" class="modal fade" role="dialog">
                <div class="modal-dialog">
                  <!-- konten modal-->
                  <div class="modal-content">
                    <!-- heading modal -->
                    <div class="modal-header">
                      <button type="button" class="close" data-dismiss="modal">&times;</button>
                      <h4 class="modal-title">Pilih Kota</h4>
                    </div>
                    <!-- body modal -->
                    <div class="modal-body container-fluid">
                      <form class="form-group">
                        <input class="form-control" placeholder="Ketikkan Nama Kota" v-model="cari" @keydown.down="onArrowDown" @keydown.up="onArrowUp" @keydown.enter.prevent="onEnter" @input="onChange">
                      </form>
                      <ul class="autocomplete-results container" v-show="isOpen" id="autocomplete-results">
                        <li
                          class="loading"
                          v-if="isLoading"
                        >
                          Loading results...
                        </li>

                        <li v-else
                          v-for="(result, i) in results"
                          :key="i"
                          @click="setResult(result)"
                          class="autocomplete-result"
                          :class="{ 'is-active': i === arrowCounter }"
                        >
                        {{result}}
                        </li>
                      </ul>
                    </div>
                    <!-- footer modal -->
                    <div class="modal-footer">
                      <button @click="pilihKota()" type="button" class="btn btn-default" data-dismiss="modal">Pilih</button>
                    </div>
                  </div>
                </div>
              </div>

            </form>
           </div>
          </div>
          <!-- bagian untuk mencetak kartu -->
        <div class="row">

            <div v-if="isWaiting" class="container">
              <p class="lead text-muted text-center py-5">tunggu yaaa . . .</p>
            </div>

            <div v-if="nothing" class="container">
              
              <div class="row justify-content-md-center">
                <img class="card-img-top img-fluid" width="100" height="100" src="static/admin-100.png">
              </div>
              <div class="row py-4">
                <p class="lead text-muted text-center col-md-12">Maaf barang dengan keyword {{item}} tidak ada. silahkan coba keyword lain</p>
              </div>
            </div>

            <div v-if="ada" class="row container">

              <div v-for="item in lessData" :key="item" class="col-lg-3 py-2">
                <div class="card" style="width: 13rem;">
                <img class="card-img-top img-fluid" v-if="item.product_image_url != null" :src="item.product_image_url" alt="Card image cap">
                <img class="card-img-top img-fluid" v-if="item.product_image_url == null" :src="gambarDefault" alt="Card image cap">
                <div class="card-block">
                  <div class="card-text">
                    <li><b>{{ item.product_name }}</b> <a style="float: right" class="text-muted">Rp.{{item.product_price}},-</a></li>
                    <li>Lokasi <b>{{item.seller_location}}</b></li>
                    <li>Reputasi : <b>{{item.seller_rating}}</b> / 10</li>
                    <li>Jumlah Terjual : <b>{{ item.product_num_sold }}</b> Dukungan Ekspedisi : <a v-b-popover.hover="''+item.seller_expeditions"><b>{{item.seller_expeditions.length}}</b></a></li>
                  </div>
                </div>
              </div>
              </div>
    
            </div>
          <div v-if="ada && !getMore"
            class="row container py-3 d-flex justify-content-center">
              <button @click="more()" class="btn btn-success text-white">Tampilkan Rekomendasi Lainnya</button>
          </div>
          <div v-if="getMore"
            class="row container">
            <div v-for="item in moreData" :key="item" class="col-lg-3 py-2">
              <div class="card" style="width: 13rem;">
                <img class="card-img-top img-fluid" v-if="item.product_image_url != null" :src="item.product_image_url" alt="Card image cap">
                <img class="card-img-top img-fluid" v-if="item.product_image_url == null" :src="gambarDefault" alt="Card image cap">
                <div class="card-block">
                  <div class="card-text">
                    <li><b>{{ item.product_name }}</b> <a style="float: right" class="text-muted">Rp.{{item.product_price}},-</a></li>
                    <li>Lokasi <b>{{item.seller_location}}</b></li>
                    <li>Reputasi : <b>{{item.seller_rating}}</b> / 10</li>
                    <li>Jumlah Terjual : <b>{{ item.product_num_sold }}</b></li>
                    <li>Dukungan Ekspedisi : <a v-b-popover.hover="''+item.seller_expeditions"><b>{{item.seller_expeditions.length}}</b></a></li>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import swal from 'sweetalert'
import axios from 'axios'
export default {
  name: 'app',
  props: {
      items: {
        type: Array,
        required: false,
        default: () => [],
      },
      isAsync: {
        type: Boolean,
        required: false,
        default: false,
      }
    },
  data () {
    return {
      statusLogin: 'Login',
      isLogin: 'btn-success',
      pilih: '',
      isOpen: false,
      results: [],
      cari: '',
      isLoading: false,
      arrowCounter: 0,
      hasLogin: false,
      price: '',
      sellerLocation: '',
      sellerRating: '',
      numProductSold: '',
      expedition: '',
      displayName: '',
      profile: {},
      kota: [],
      data: [],
      lessData: [],
      moreData: [],
      ada: false,
      getMore: false,
      toko: 'tokopedia',
      akses: false,
      nothing: false,
      item: '',
      isWaiting: false,
      gambarDefault: 'static/default.jpg'
    }
  },
  methods: {
    // fungsi untuk autocomplete memilih kota
    pilihKota() {
      this.pilih = this.cari
    },
    onChange() {
      
      this.$emit('input', this);

      // apakah digunakan ketika AJAX request
      if (this.isAsync) {
        this.isLoading = true;
      } else {
        // biarkan flat array kita
        this.filterResults();
        this.isOpen = true;
      }
    },
    filterResults() {
      // buat semua data menjadi kapital (menyesuaikan data json)
      this.results = this.kota.filter((item) => {
        return item.toUpperCase().indexOf(this.cari.toUpperCase()) > -1;
      });
    },
    setResult(result) {
      this.cari = result;
      this.isOpen = false;
    },
    onArrowDown(evt) {
      if (this.arrowCounter < this.results.length) {
        this.arrowCounter = this.arrowCounter + 1;
      }
    },
    onArrowUp() {
      if (this.arrowCounter > 0) {
        this.arrowCounter = this.arrowCounter -1;
      }
    },
    onEnter() {
      this.cari = this.results[this.arrowCounter];
      this.isOpen = false;
      this.arrowCounter = -1;
    },
    handleClickOutside(evt) {
      if (!this.$el.contains(evt.target)) {
        this.isOpen = false;
        this.arrowCounter = -1;
      }
    },
    //fungsi untuk melakukan pencarian (untuk mencari barang)
    search() {
      let lokasiSesuai = false
      this.kota.forEach((el) => {
        if(el == this.$refs.currentLocation.value) lokasiSesuai = true
      })

      let sama = 0
      let pembanding = []
      
      pembanding.push(this.price)
      pembanding.push(this.sellerLocation)
      pembanding.push(this.sellerRating)
      pembanding.push(this.numProductSold)
      pembanding.push(this.expedition)

      //menguji setiap data dari variabel pembanding
      for(let i=0; i<pembanding.length; i++) {
        for(let j=0; j<pembanding.length; j++) {
          if(pembanding[i] == pembanding[j] && i != j) {
            sama++ // sama = sama + 1
          }
        }
      }

      // menguji apakah setiap data prioritas kosong atau tidak
      if(this.price != '' && this.sellerLocation != '' && this.sellerRating != this.numProductSold && this.expedition != '') {
        // menguji apakah kolom keyword barang dan lokasi masih kosong
        if(this.$refs.item.value != '' && this.$refs.currentLocation.value != '') {    
          //jika lokasi tidak ada yang sesuai dengan data yang ada di json maka akan mengembalikan nilai default berupa true
          if(lokasiSesuai) {
            // jika sama lebih dari 0 maka akan salah
            if(!sama) {

                // alert(`kamu mencari ${this.$refs.item.value} di lokasi ${this.$refs.currentLocation.value} pada olshop ${this.toko}`)
                this.isWaiting = true
                this.nothing = false
                this.getMore = false
                this.ada = false

                sessionStorage.setItem('sellerLocation', this.$refs.currentLocation.value)
                sessionStorage.setItem('price', this.price)
                sessionStorage.setItem('numProductSold', this.numProductSold)
                sessionStorage.setItem('sellerRating', this.sellerRating)
                sessionStorage.setItem('sellerLocation', this.expedition)
                sessionStorage.setItem('expedition', this.sellerLocation)

                // this.lessData = this.data.slice(0,4);
                // this.getMore = false
                // this.ada = true
              
              axios.post('https://reco-saw.herokuapp.com/search', {
                  username: this.profile['username'] || null,
                  location: this.$refs.currentLocation.value,
                  keyword: this.$refs.item.value,
                  shop_name: this.toko,
                  pri_product_price: parseInt(this.price),
                  pri_product_num_sold: parseInt(this.numProductSold),
                  pri_seller_rating: parseInt(this.sellerRating),
                  pri_seller_expeditions: parseInt(this.expedition),
                  pri_seller_location: parseInt(this.sellerLocation)
              }).then(response => {
                console.log(response.data.data)
                this.data = response.data.data
                console.log(this.data[0].product_image_url)
                  this.isWaiting = true
                if(this.data.length != 0) {
                  // this.barangBaru()
                  this.isWaiting = false
                  console.log('ga sukses')
                  this.lessData = this.data.slice(0,4);
                  this.getMore = false
                  this.ada = true
                } else {
                  swal('Pencarian Gagal', 'Barang yang anda cari tidak ada', 'warning')
                  this.nothing = true
                  this.isWaiting = false
                }
              }).catch(err => {
                console.log(err)
                swal('Pencarian Gagal', 'Barang yang anda cari tidak ada', 'warning')
                this.nothing = true
                this.isWaiting = false
              })

            } else {
              swal('Prioritas Salah', 'Data prioritas tidak boleh ada yang sama', 'warning')

              pembanding = null
            }

          } else {
            swal('Kabupaten tidak ada', 'Mohon periksa kembali kabupaten tujuan anda', 'warning')
          }
        } else {
          swal('Data Masih Kosong', 'Mohon periksa form keyword barang dan lokasi', 'warning')
        }
      } else {
        swal('Data Prioritas Salah', 'Prioritas tidak boleh kosong', 'warning')
      }
    },
    //fungsi untuk memasukan jumlah kedalam variabel moreData
    more() {
      //akan menampilkan data yang lebih dari 5
      this.moreData = this.data.slice(4);
      this.getMore = true;
      this.moreData.forEach(el => {
        console.log(el)
      })
    },
    // fungsi untuk melakukan login (menggunakan username dan password)
    login() {
      //username dan password tidak boleh kosong
      if(this.$refs.username.value != '' && this.$refs.password.value != '') {
        // axios.get('http://localhost:3002/data')

        axios.post('http://reco-saw.herokuapp.com/login', {
          username: this.$refs.username.value,
          password: this.$refs.password.value

        }).then(res => {
          // console.log(res)
          console.log(res.data.data)
          // console.log(res.data.message)
          this.profile = res.data.data
          this.hasLogin = true

          this.isLogin = 'btn-danger'
          this.statusLogin = 'Logout'
          swal('Login Sukses', 'Anda Berhasil Masuk', 'success')
          sessionStorage.setItem('displayName', res.data.data['display_name']);
          sessionStorage.setItem('username', res.data.data['username']);
          sessionStorage.setItem('password', this.$refs.password.value);
          sessionStorage.setItem('price', res.data.data['pri_product_price'])
          sessionStorage.setItem('numProductSold', res.data.data['pri_product_num_sold'])
          sessionStorage.setItem('sellerRating', res.data.data['pri_seller_rating'])
          sessionStorage.setItem('sellerLocation', res.data.data['pri_seller_location'])
          sessionStorage.setItem('expedition', res.data.data['pri_seller_expeditions'])

          //session untuk fungsional aplikasi
          sessionStorage.setItem('hasLogin', this.hasLogin)
          sessionStorage.setItem('statusLogin', this.statusLogin)
          sessionStorage.setItem('isLogin', this.isLogin)
          this.initialized()
        }).catch(err => {
          console.log(err)
          swal('Login Gagal', 'Periksa Kembali Username dan Password Anda.', 'success')
          this.hasLogin = false
          this.initialized()
        })

      } else {
        swal('Login Gagal', 'Periksa kembali username dan password anda', 'warning')
      }
    },
    logout() {
      //akan digunakan untuk men-destroy session
      sessionStorage.clear();

      //hapus semua data, kembalikan menjadi default
      swal('Terimakasih', 'Anda telah berhasil keluar', 'success')

      //kembalikan data seperti semula
      this.hasLogin = false
      this.$refs.username.value = ''; this.$refs.password.value = '';
      this.initialized()
    },
    registrasi() {
      //membutuhkan data username (email), display name, password
      if(this.$refs.usernameReg.value != '' && this.$refs.passwordReg.value != '' && this.$refs.displayNameReg.value != '') {

        swal('Berhasil', 'berhasil di daftar ceritanya', 'success')
        //digunakan untuk mengirim data calon pendaftar
        // axios.post('http://localhost:3000/register', {
        //   username: this.$refs.usernameReg.value,
        //   password: this.$refs.passwordReg.value,
        //   display_name: this.$refs.displayNameReg.value
        // }).then((res) => {
        //   swal('Terimakasih', 'Mohon periksa email anda !', 'success')
        //   console.log(res)
        // })

      } else {
        swal('Registrasi Gagal', 'Mohon periksa kembali isi form yang ada', 'warning')
      }
      
      // swal('Registrasi', 'Fitur akan segera dibuat', 'success')
    },
    lupaPassword() {
      //membutuhkan username (email), kemudian akan mengirimkan password ke email
      if(this.$refs.emailLostPassword.value != '') {
        swal('Masih Bingung', 'Harus ada mailer pada backend', 'success')
      } else {
        swal('Gagal', 'Kolom email tidak boleh kosong', 'warning')
      }
      // swal('Lupa Password', 'Fitur akan segera dibuat', 'success')
    },
    about() {
      //akan memberi informasi tentang website
      swal('About', 'Fitur akan segera dibuat', 'success')
    },
    initialized() {
        //jika sudah login atau ada session username
        if(this.hasLogin || sessionStorage.getItem('username')) {

        //data profile pengguna
        this.displayName = this.profile['display_name'] || sessionStorage.getItem('displayName')

        //data prioritas
        this.price = this.profile['pri_product_price'] || sessionStorage.getItem('price')
        this.numProductSold = this.profile['pri_product_num_sold'] || sessionStorage.getItem('numProductSold')
        this.sellerRating = this.profile['pri_seller_rating'] || sessionStorage.getItem('sellerRating')
        this.sellerLocation = this.profile['pri_seller_location'] || sessionStorage.getItem('sellerLocation')
        this.expedition = this.profile['pri_seller_expeditions'] || sessionStorage.getItem('expedition')

        //status login
        this.hasLogin = sessionStorage.getItem('hasLogin') || 'false'
        this.statusLogin = sessionStorage.getItem('statusLogin') || 'Login'
        this.isLogin = sessionStorage.getItem('isLogin') || 'btn-success'
      } else {
        this.displayName = 'Guest'
        this.price = ''; this.numProductSold = ''; this.sellerRating = ''; this.sellerLocation = ''; this.expedition = '';
        this.statusLogin = 'Login'
        this.isLogin = 'btn-success'
      }

    },
    barangBaru() {
      //data barang
      // axios.get('http://localhost:3000/data')
      axios.get('http://api.jsonbin.io/b/5b699b382b23fb1f2b7089be')
      .then(res => {
        console.log('data sukses')
        // this.data = res.data['data']
        // this.akses = true

        this.lessData = this.data.slice(0,4);
        this.getMore = false
        this.ada = true
      })
      .catch(e => {
        this.errors.push(e)
        console.log('gagal')
        swal('Pencarian Gagal', 'Barang yang anda cari tidak ada', 'warning')
        this.nothing = true
      })
    }
  },
  update() {
    // this.barangBaru()
    $nextTick(() => {
      // this.barangBaru()
    })
  },
  created() {
    // console.log('berhasil masuk ke dalam created')

    //data profile pengguna
    // axios.get('http://localhost:3002/data')
    // .then(res => {
    //   // console.log('data sukses')
    //   this.profile = res.data
    //   this.hasLogin = true
    //   this.initialized()
    // })
    // .catch(e => {
    //   // this.errors.push(e)
    //   this.hasLogin = false
    //   this.initialized()
    // })

    this.initialized()

    //data kabupaten indonesia
    // axios.get('http://localhost:3001/data')
    axios.get('http://api.jsonbin.io/b/5b7431c47b21295367910fb5/2')
    .then(res => {
      // console.log('data sukses')
      this.kota = res.data['data']
      // console.log(res.data['data'])
    })
    .catch(e => {
      this.errors.push(e)
    })
  },
  mounted() {
    document.addEventListener('click', this.handleClickOutside)
  },
  destroyed() {
    document.removeEventListener('click', this.handleClickOutside)
  },
  watch: {
    items: function (val, oldValue) {
      // bandingkan variabel untuk autocomplete
      if (val.length !== oldValue.length) {
        this.results = val;
        this.isLoading = false;
      }
    },
  },
}
</script>

<style>
  /*@import 'https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-alpha.6/css/bootstrap.min.css';*/

  .autocomplete {
    position: relative;
  }

  .autocomplete-results {
    padding: 0;
    margin: 0;
    border: 1px solid #eeeeee;
    height: 120px;
    overflow: auto;
    width: 100%;
  }

  .autocomplete-result {
    list-style: none;
    text-align: left;
    padding: 4px 2px;
    cursor: pointer;
  }

  .autocomplete-result.is-active,
  .autocomplete-result:hover {
    background-color: #4AAE9B;
    color: white;
  }

  .tombol {
    padding: 0;
    width: 63px;
    height: 63px;
  }

  .m-y-25 {
    margin-top: -25px;
  }

  .m-x-10 {
    margin-right: -10px;
  }

  .m-x-5 {
    margin-left: 10px;
    margin-right: 30px;
  }

  .link {
    color: #0275d8;
  }

  li {
    list-style-type: none;
    font-size: 0.9em;
  }
</style>


<!-- target berikutnya adalah logout / login / register function -->
<!-- kemudian buat session pada login / logout -->
<!-- perbaiki bug pada system C:/documents/AIGame/file nya -->