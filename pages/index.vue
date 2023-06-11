<template>
  <section class="section">
    <div class="container">
      <div class="columns is-mobile is-centered">
        <div class="column is-full">
          <div class="box">

            <h1>Selamat Datang, {{ user.data.nama_guru }}!</h1>
          </div>
          <div class="field has-addons">
            <div class="control">
              <input class="input" type="text" placeholder="Cari Absen">
            </div>
            <div class="control">
              <a class="button is-info">
                Cari
              </a>
            </div>
          </div>
        </div>
      </div>

      <div class="columns is-multiline is-mobile">
        <div class="column is-half" v-for="(item, index) in posts" :key="item.id">
          <div class="box">
            <h3>{{ item.nama_matapelajaran }}, {{ user.data.nama_guru }}!</h3>
            <p></p>
            <p>{{ item.hari }}</p>
            <p>jam awal-jam akhir | jumlah jam</p>
            <p>{{ user.data.nama_guru }}</p>
            <p>{{ item.status }}</p>
            <button class="button is-info ">Absen</button>
            <button class="button is-warning">Edit</button>
            <button class="button is-danger ">Hapus</button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      user: this.$auth.user,
      posts: [],
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.$nuxt.$loading.start()
      this.$axios.get('http://localhost:8000/api/jadwal').then((res) => {
        this.posts = res.data.data
      })
    })
  },
  methods: {
    async logout() {
      await this.$auth.logout()

      this.$router.push('/login')
    },

  },
}
</script>