<template>
  <div>

    <div class="section">
      <div class="container">
        <div class="columns">
          <div class="column is-6 is-offset-3">

            <div class="field">
              <label class="label">Pencarian Teman</label>
              <div class="columns">
                <div class="column is-8">
                  <input type="text" class="input" v-model="searchQuery">
                </div>
                <div class="column is-4">
                  <button class="button is-primary is-outlined is-fullwidth" v-on:click="getSearchUser">Search</button>
                </div>
              </div>
            </div>
            <div class="tabs is-centered is-boxed is-fullwidth">
              <ul>
                <li v-bind:class="[isActive ? activeClass : '', errorClass]" v-on:click="changeTab">
                  <a>
                    <span class="icon is-small"><i class="fas fa-user" aria-hidden="true"></i></span>
                    <span>Cari Teman</span>
                  </a>
                </li>
                <li v-bind:class="[isActive ? '' : activeClass, errorClass]" v-on:click="changeTab">
                  <a>
                    <span class="icon is-small"><i class="fas fa-user-friends" aria-hidden="true"></i></span>
                    <span>Teman Saya</span>
                  </a>
                </li>
              </ul>
            </div>
<!--            <div class="notification is-success">-->
<!--              <p>Permintaan pertemanan berhasil di tambahkan.</p>-->
<!--            </div>-->

            <div v-if="isActive">
              <div class="box" v-for="(user, index) in users">
                <div class="columns">
                  <div class="column is-2 has-text-centered is-horizontal-center">
                    <div class='is-flex is-horizontal-center'>
                      <figure class="image is-64x64 has-text-centered">
                        <img class="is-rounded" :src="user.image ? user.image : 'https://bulma.io/images/placeholders/128x128.png'">
                      </figure>
                    </div>
                  </div>
                  <div class="column is-7">
                    <span class="subtitle">{{ user.firstName + " " + user.lastName }} </span>
                    <br><span>@{{ user.username }}</span>
                  </div>
                  <div class="column is-3">
                    <div class="container">
                      <button class="button is-rounded is-small is-primary" v-on:click="addUser(user.id)">Tambah Teman</button>
                    </div>
                  </div>
                </div>
              </div>

            </div>
            <div v-if="isActive == false">
              <div class="box" v-for="(user, index) in userFriends">
                <div class="columns">
                  <div class="column is-2 has-text-centered is-horizontal-center">
                    <div class='is-flex is-horizontal-center'>
                      <figure class="image is-64x64 has-text-centered">
                        <img class="is-rounded" :src="user.image ? user.image : 'https://bulma.io/images/placeholders/128x128.png'">
                      </figure>
                    </div>
                  </div>
                  <div class="column is-7">
                    <span class="subtitle">{{ user.firstName + " " + user.lastName }} </span>
                    <br><span>@{{ user.username }}</span>
                  </div>
                  <div class="column is-3">
                    <div class="container">
                      <button class="button is-rounded is-small is-outlined is-primary" v-on:click="showUserInvestment(user)">Lihat Investasi</button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <hr>
            <div v-if="showInvestment">
              <div class="box">
                <div class="columns">
                  <div class="column is-2 has-text-centered is-horizontal-center">
                    <div class='is-flex is-horizontal-center'>
                      <figure class="image is-64x64 has-text-centered">
                        <img class="is-rounded" :src="userSingle.image ? userSingle.image : 'https://bulma.io/images/placeholders/128x128.png'">
                      </figure>
                    </div>
                  </div>
                  <div class="column is-10">
                    <span class="subtitle">{{ userSingle.firstName + " " + userSingle.lastName }} </span>
                    <br><span>@{{ userSingle.username }}</span>
                  </div>
                </div>
              </div>
              <div class="box">
                <h2 class="subtitle">Informasi Investasi Terbaru</h2>
                <table class="table is-bordered is-fullwidth">
                  <thead>
                  <th>No</th>
                  <th>Judul Investasi</th>
                  <th>Jenis Investasi</th>
                  <th>Tanggal</th>
                  </thead>
                  <tbody>
                  <tr>
                    <td colspan="4">tidak ada data</td>
                  </tr>
<!--                  <tr>-->
<!--                    <td>1</td>-->
<!--                    <td>Pembukaan Soto Ayam</td>-->
<!--                    <td>Proyek</td>-->
<!--                    <td>25 Februari 2018</td>-->
<!--                  </tr>-->
<!--                  <tr>-->
<!--                    <td>2</td>-->
<!--                    <td>Sate Sapi dan Kelinci pak Gendut</td>-->
<!--                    <td>Saham</td>-->
<!--                    <td>01 Maret 2018</td>-->
<!--                  </tr>-->
                  </tbody>
                </table>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        isActive: true,
        activeClass: 'is-active',
        errorClass: '',
        users: [],
        userFriends: [],
        searchQuery: '',
        showInvestment: false,
        userSingle: ''
      }
    },
    mounted() {
      this.getUsers()
      this.getUserFriends()
    },
    methods: {
      changeTab() {
        if (this.isActive) {
          this.isActive = false;
        } else {
          this.isActive = true;
        }
        this.getUserFriends()
        this.getUsers()
      },
      getUsers() {
        this.$axios.get('/core/users/').then(response => {
          this.users = response.data.results
          console.log(this.users)
        })
      },
      getUserFriends() {
        this.$axios.get('/core/users/connections/').then(response => {
          this.userFriends = response.data.results
          console.log(this.userFriends)
        })
      },
      getSearchUser() {
        this.$axios.get('/core/users/?search=' + this.searchQuery).then(response => {
          this.users = response.data.results
          console.log(this.users)
        })
      },
      addUser(idUser) {
        this.$axios.post('/core/users/' + idUser + '/add/').then(response => {
          console.log(response.data)
          this.getUsers();
          this.getUserFriends();
        })
      },
      showUserInvestment(user) {
        this.showInvestment = true;
        this.getUserProfileDetail(user)
      },
      getUserProfileDetail(user) {
        this.userSingle = user;
      }
    },
  }
</script>
