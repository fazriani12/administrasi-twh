<template>
    <section class="section">
        <div class="container">
            <div class="columns is-mobile is-centered">
                <div class="column is-full">
                    <div class="box">
                        <h1>Daftar Matapelajaran</h1>
                    </div>
                    <div class="column">
                        <nuxt-link to="/matapelajaran/create"><button class="button is-success is-medium">
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


            <div class="columns is-multiline is-desktop is-mobile">
                <div class="column is-half" v-for="(item, index) in matapelajarans" :key="item.id">
                    <div class="box">
                        <h3>{{ item.nama_matapelajaran }}</h3>
                        <p>{{ item.nama_kelas }}</p>
                        <p>{{ item.nama_guru }}</p>
                        <p>{{ item.status }}</p>
                        <nuxt-link to="/absen" class="btn btn-info mr-2"><button
                                class="button is-info is-info">Absen</button></nuxt-link>
                        <nuxt-link :to="`/matapelajaran/edit/${item.id}`" class="btn btn-info mr-2"><button
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
            matapelajarans: [],
        }
    },
    mounted() {
        this.$nextTick(() => {
            this.$nuxt.$loading.start()
            this.$axios.get('http://localhost:8000/api/matapelajaran').then((res) => {
                this.matapelajarans = res.data.data
            })
        })
    },

    methods: {
        async hapus(id) {
            await this.$axios.delete('http://localhost:8000/api/matapelajaran/' + id).then((res) => {
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