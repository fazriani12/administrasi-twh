<template>
    <section class="section">
        <div class="container">
            <div class="columns is-mobile is-centered">
                <div class="column is-full">
                    <div class="box">
                        <h1>Tambah Jadwal Baru</h1>
                    </div>
                </div>
            </div>
            <form @submit="handleSubmit">
                <p>{{ selectedMapel }}</p>
                <div class="field">
                    <label class="label">Nama Matapelajaran</label>
                    <div class="select is-info">
                        <select v-model="selectedMapel">
                            <option v-for="(item) in matapelajarans" :key="item.id" v-bind:value="item.id">
                                {{
                                    item.nama_matapelajaran
                                }}</option>
                        </select>
                    </div>
                </div>

                <p>{{ selectedKelas }}</p>
                <div class="field">
                    <label class="label">Kelas</label>
                    <div class="select is-info">
                        <select v-model="selectedKelas">
                            <option v-for="(item) in kelas" :key="item.id" v-bind:value="item.id">{{ item.nama_kelas
                            }}</option>
                        </select>
                    </div>
                </div>


                <p>{{ selectedGuru }}</p>
                <div class="field">
                    <label class="label">Guru</label>
                    <div class="select is-info">
                        <select v-model="selectedGuru">
                            <option v-for="(item) in guru" :key="item.id" v-bind:value="item.id">{{ item.nama_guru
                            }}</option>
                        </select>
                    </div>
                </div>

                <div class="field">
                    <label class="label">Tahun</label>
                    <div class="control">
                        <input class="input is-info" v-model="post.tahun" type="text" placeholder="Text input">
                    </div>
                </div>

                <div class="field">
                    <label class="label">Bulan</label>
                    <div class="control">
                        <input class="input is-info" v-model="post.bulan" type="text" placeholder="Text input">
                    </div>
                </div>
                <div class="field">
                    <label class="label">Tanggal</label>
                    <div class="control">
                        <input class="input is-info" v-model="post.tanggal" type="text" placeholder="Text input">
                    </div>
                </div>
                <p>{{ selectedSiswa }}</p>
                <div class="field">
                    <label class="label">Siswa</label>
                    <div class="select is-info">
                        <select v-model="selectedSiswa">
                            <option v-for="(item) in siswa" :key="item.id" v-bind:value="item.id">{{ item.nama_siswa
                            }}</option>
                        </select>
                    </div>
                </div>
                <div class="field">
                    <label class="label">Kehadiran</label>
                    <div class="select is-info">
                        <select v-model="selectedAbsensi">
                            <option value="1">1</option>
                            <option value="s">s</option>
                            <option value="i">i</option>
                            <option value="a">a</option>
                        </select>
                    </div>
                </div>
                <div class="field">
                    <label class="label">Pokok Bahasan</label>
                    <div class="control">
                        <input class="input is-info" v-model="post.pokok_bahasan" type="text" placeholder="Text input">
                    </div>
                </div>

                <div class="field is-grouped">
                    <div class="control">
                        <button class="button is-success" type="submit">Submit</button>
                    </div>
                    <div class="control">
                        <nuxt-link to="/jadwal"><button class="button is-light">
                                Cancel</button></nuxt-link>
                    </div>
                </div>
            </form>
        </div>
    </section>
</template>
<script>
export default {
    data() {
        return {
            post: {
                matapelajarans_id: null,
                kelas_id: null,
                gurus_id: null,
                siswas_id: null,
                tahun: null,
                bulan: null,
                tanggal: null,
                absensi: null,
                pokok_bahasan: null

            },
            matapelajarans: [],
            selectedMapel: null,
            kelas: [],
            selectedKelas: null,
            guru: [],
            selectedGuru: null,
            siswa: [],
            selectedSiswa: null,
            selectedAbsensi: null


        }
    },
    mounted() {
        this.$nextTick(() => {
            this.$nuxt.$loading.start()
            this.$axios.get('http://localhost:8000/api/absen').then((res) => {
                this.absens = res.data.data
            })
            this.$axios.get('http://localhost:8000/api/matapelajaran').then((res) => {
                this.matapelajarans = res.data.data
            })
            this.$axios.get('http://localhost:8000/api/kelas').then((res) => {
                this.kelas = res.data.data
            })

            this.$axios.get('http://localhost:8000/api/guru').then((res) => {
                this.guru = res.data.data
            })
            this.$axios.get('http://localhost:8000/api/siswa').then((res) => {
                this.siswa = res.data.data
            })
        })
    },
    methods: {
        async handleSubmit(event) {
            const formData = new FormData()
            event.preventDefault();
            formData.append('matapelajarans_id', this.selectedMapel)
            formData.append('tahun', this.post.tahun)
            formData.append('bulan', this.post.bulan)
            formData.append('tanggal', this.post.tanggal)
            formData.append('kelas_id', this.selectedKelas)
            formData.append('siswas_id', this.selectedSiswa)
            formData.append('gurus_id', this.selectedGuru)
            formData.append('absensi', this.selectedHari)
            await this.$axios.post('http://localhost:8000/api/jadwal', formData).then((res) => {
                if (res.status === 200) {
                    this.$router.go(-1)
                } else {
                    console.log(res)
                }
                console.log(res)
            })
        }
    }
}
</script>

