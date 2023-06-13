<template>
    <section class="section">
        <div class="container">
            <div class="columns is-mobile is-centered">
                <div class="column is-full">
                    <div class="box">
                        <h1>Daftar Nama Kelas</h1>
                    </div>
                    <div class="column">
                        <nuxt-link to="/kelas/create"><button class="button is-success is-medium">
                                + Tambah Data</button></nuxt-link>
                    </div>
                    <div class="field has-addons">
                        <div class="control">
                            <input class="input" type="text" placeholder="Find a repository">
                        </div>
                        <div class="control">
                            <a class="button is-info">
                                Search
                            </a>
                        </div>
                    </div>
                </div>
            </div>
            <table class="table">
                <thead>
                    <tr>
                        <th><abbr title="kelas_id">Kode Kelas</abbr></th>
                        <th><abbr title="nama_kelas">Nama Kelas</abbr></th>
                        <th><abbr>Tindakan</abbr></th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(item, Kelas) in posts" :key="item.id">
                        <th>{{ Kelas + 1 }}</th>
                        <td>{{ item.nama_kelas }}</td>
                        <td><nuxt-link :to="`/kelas/edit/${item.id}`" class="btn btn-info mr-2"><button
                                    class="button is-warning">Edit</button></nuxt-link>
                            <button @click="hapus(item.id)" class="button is-danger ">Hapus</button>
                        </td>
                    </tr>
                </tbody>
            </table>
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
            this.$axios.get('http://localhost:8000/api/kelas').then((res) => {
                this.posts = res.data.data
            })
        })
    },
    methods: {
        async hapus(id) {
            await this.$axios.delete('http://localhost:8000/api/kelas/' + id).then((res) => {
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

