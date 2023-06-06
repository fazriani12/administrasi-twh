<template>
    <section class="section">
        <div class="container">
            <div class="columns is-mobile is-centered">
                <div class="column is-full">
                    <div class="box">
                        <h1>Absen {Kelas}</h1>
                        <h1>Mapel : {Matapelajaran}</h1>
                        <h1>Guru : {Nama Guru}</h1>
                    </div>
                    <div class="column">
                        <button class="button is-success is-normal">+ Tambah Siswa</button>
                        <button class="button is-warning is-normal">Edit</button>
                    </div>
                </div>
            </div>

            <div class="columns">
                <div class="column box is-1">
                    No
                </div>
                <div class="column box is-3">
                    Nama
                </div>
                <div class="column box is-2">
                    NIS
                </div>
                <div class="column box is-4">
                    Tanggal
                    <div class="columns is-mobile">
                        <div class="column">1</div>
                        <div class="column">2</div>
                        <div class="column">3</div>
                        <div class="column">4</div>
                    </div>
                </div>
                <div class="column box is-2">
                    Materi Pelajaran
                </div>
            </div>
            <div class="columns">
                <div class="column box">
                    1
                </div>
                <div class="column box is-2">
                    Pokok Bahasan
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
        }
    },
    Mounted: () => {
        console.log('test')

    },
    methods: {
        async logout() {
            await this.$auth.logout()

            this.$router.push('/login')
        },

    },
}
</script>