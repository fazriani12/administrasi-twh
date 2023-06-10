<template>
    <section class="section">
        <div class="container">
            <div class="columns is-mobile is-centered">
                <div class="column is-full">
                    <div class="box">
                        <h1>Daftar Matapelajaran</h1>
                    </div>
                    <div class="column">
                        <button class="button is-success is-medium">+ Tambah Data</button>
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
                        <p>Hari</p>
                        <p>jam awal-jam akhir | jumlah jam</p>
                        <p>{{ item.nama_guru }}</p>
                        <p>Status Matapelajaran</p>
                        <button class="button is-info is-info">Absen</button>
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

    computed: {

    },

    methods: {
        async logout() {
            await this.$auth.logout()

            this.$router.push('/login')
        },



    },
}
</script>