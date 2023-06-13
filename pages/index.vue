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
            <p>{{ item.kelas }}</p>
            <p>{{ item.hari }}</p>
            <p>{{ item.jam_awal }} - {{ item.jam_akhir }} | {{ jml_jam }}</p>
            <p>{{ user.data.nama_guru }}</p>
            <nuxt-link :to="`/absen/${item.id}`" class="btn btn-info mr-2"><button
                class="button is-info is-info">Absen</button></nuxt-link>
            <nuxt-link :to="`/jadwal/edit/${item.id}`" class="btn btn-info mr-2"><button
                class="button is-warning">Edit</button></nuxt-link>
            <button @click="hapus(item.id)" class="button is-danger ">Hapus</button>
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
    async hapus(id) {
      await this.$axios.delete('http://localhost:8000/api/jadwal/' + id).then((res) => {
        if (res.status === 200) {
          this.$router.go(0)
        } else {
          console.log(res)
        }
        console.log(res)
      })
    }
  }
}
</script>