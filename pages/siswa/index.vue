<template>
    <section class="section">
        <div class="container">
            <div class="columns is-mobile is-centered">
                <div class="column is-full">
                    <div class="box">
                        <h1>Daftar Nama Siswa</h1>
                    </div>
                    <div class="column">
                        <nuxt-link to="/siswa/create"><button class="button is-success is-medium">
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
                        <th><abbr title="siswas_id">No</abbr></th>
                        <th><abbr title="nama_siswa">Nama Siswa</abbr></th>
                        <th><abbr title="nis">NIS</abbr></th>
                        <th><abbr title="kelas_id">Kelas</abbr></th>
                        <th><abbr>Action</abbr></th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(item, index) in siswas" :key="item.id">
                        <th>{{ index + 1 }}</th>
                        <td>{{ item.nama_siswa }}</td>
                        <td>{{ item.nis }}</td>
                        <td>{{ item.nama_kelas }}</td>
                        <td><nuxt-link :to="`/siswa/edit/${item.id}`" class="btn btn-info mr-2"><button
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
            siswas: [],
        }
    },
    mounted() {
        this.$nextTick(() => {
            this.$nuxt.$loading.start()
            this.$axios.get('http://localhost:8000/api/siswa').then((res) => {
                this.siswas = res.data.data
            })
        })
    },
    methods: {
        async hapus(id) {
            await this.$axios.delete('http://localhost:8000/api/siswa/' + id).then((res) => {
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

