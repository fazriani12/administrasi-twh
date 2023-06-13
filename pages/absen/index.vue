<template>
    <section class="section">
        <div class="container">
            <div class="columns is-mobile is-centered">
                <div class="column is-full">
                    <div class="box" v-for="(item, index) in absens" :key="item.id">
                        <h1>{{ item.nama_kelas }}</h1>
                        <h1>Mapel : {Matapelajaran}</h1>
                        <h1>Guru : {Nama Guru}</h1>
                    </div>
                    <div class="column">
                        <button class="button is-success is-normal">+ Tambah Siswa</button>
                        <button class="button is-warning is-normal">Edit</button>
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
            absens: [],
        }
    },
    Mounted: () => {
        this.$nextTick(() => {
            this.$nuxt.$loading.start()
            this.$axios.get('http://localhost:8000/api/absen').then((res) => {
                this.absens = res.data.data
            })
        })

    },
    methods: {
        async logout() {
            await this.$auth.logout()

            this.$router.push('/login')
        },
        async hapus(id) {
            await this.$axios.delete('http://localhost:8000/api/absen/' + id).then((res) => {
                if (res.status === 200) {
                    this.$router.go(0)
                } else {
                    console.log(res)
                }
                console.log(res)
            })
        }

    },
}
</script>