<template>
    <section class="section">
        <div class="container">
            <div class="columns is-mobile is-centered">
                <div class="column is-full">
                    <div class="box">
                        <h1>Edit Jadwal</h1>
                    </div>
                </div>
            </div>
            <form @submit="handleSubmit">
                <p>{{ selectedMapel }}</p>
                <div class="field">
                    <label class="label">Nama Matapelajaran</label>
                    <div class="select is-info">
                        <select v-model.lazy="selectedMapel">
                            <option :value="null" selected>{{ post.nama_matapelajaran }}</option>
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

                        <select v-model.lazy="selectedKelas" @click="show">
                            <option :value="null" selected>{{ post.nama_kelas }}</option>
                            <option v-for="(item) in kelas" :key="item.id" v-bind:value="item.id">{{ item.nama_kelas
                            }}</option>
                        </select>
                    </div>
                </div>

                <p>{{ selectedGuru }}</p>
                <div class="field">
                    <label class="label">Guru</label>
                    <div class="select is-info">
                        <select v-model="selectedGuru" @click="show">
                            <option :value="null" selected>{{ post.nama_guru }}</option>
                            <option v-for="(item) in guru" :key="item.id" v-bind:value="item.id">{{ item.nama_guru
                            }}</option>
                        </select>
                    </div>
                </div>

                <div class="field">
                    <label class="label">Hari</label>
                    <div class="select is-info">
                        <select v-model="selectedHari">
                            <option :value="null" selected>{{ post.hari }}</option>
                            <option value="Senin">Senin</option>
                            <option value="Selasa">Selasa</option>
                            <option value="Rabu">Rabu</option>
                            <option value="Kamis">Kamis</option>
                            <option value="Jumat">Jumat</option>
                        </select>
                    </div>
                </div>

                <div class="field">
                    <label class="label">Status Matapelajaran</label>
                    <div class="select is-info">
                        <select v-model="selectedStatus" @click="show">
                            <option :value="null" selected>{{ post.status }}</option>
                            <option value="Produktif">Produktif</option>
                            <option value="Nonproduktif">Nonproduktif</option>
                        </select>
                    </div>
                </div>


                <div class="field">
                    <div class="control">
                        <label class="label">Jam Awal</label>
                        <div class="control">
                            <input class="input is-info" v-model="post.jam_awal" type="time" id="timeInput">
                        </div>
                    </div>
                </div>

                <div class="field">
                    <div class="control">
                        <label class="label">Jam Akhir</label>
                        <div class="control">
                            <input class="input is-info" v-model="post.jam_akhir" type="time" id="timeInput">
                        </div>
                    </div>
                </div>

                <div class="field">
                    <div class="control">
                        <label class="label">Jumlah Jam</label>
                        <div class="control">
                            <input class="input is-info" v-model="post.jml_jam" type="textinput">
                        </div>
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
            postId: this.$route.params.id,
            post: {
                id: null,
                nama_matapelajaran: null,
                matapelajarans_id: null,
                nama_kelas: null,
                kelas_id: null,
                nama_guru: null,
                gurus_id: null,
                hari: null,
                status: null,
                jam_awal: null,
                jam_akhir: null,
                jml_jam: null
            },
            matapelajarans: [],
            selectedMapel: null,
            kelas: [],
            selectedKelas: null,
            guru: [],
            selectedGuru: null,
            selectedStatus: null,
            selectedHari: null
        };
    },
    mounted() {

        this.$nextTick(() => {
            this.$nuxt.$loading.start()
            this.$axios.get('http://localhost:8000/api/matapelajaran').then((res) => {
                this.matapelajarans = res.data.data
            })
            this.$axios.get('http://localhost:8000/api/kelas').then((res) => {
                this.kelas = res.data.data
            })

            this.$axios.get('http://localhost:8000/api/guru').then((res) => {
                this.guru = res.data.data
            })
            this.$axios.get('http://localhost:8000/api/jadwal/' + this.postId).then((res) => {
                this.post = res.data.data[0]
            })
        })
    },
    methods: {
        async handleSubmit(event) {
            const formData = new FormData()
            event.preventDefault();
            formData.append('jam_awal', this.post.jam_awal)
            formData.append('jam_akhir', this.post.jam_akhir)
            formData.append('jml_jam', this.post.jml_jam)
            if (this.selectedMapel === null) {
                formData.append('matapelajarans_id', this.post.matapelajarans_id)
            } else {
                formData.append('matapelajarans_id', this.selectedMapel)
            }
            if (this.selectedKelas === null) {
                formData.append('kelas_id', this.post.kelas_id)
            } else {
                formData.append('kelas_id', this.selectedKelas)
            }
            if (this.selectedGuru === null) {
                formData.append('gurus_id', this.post.gurus_id)
            } else {
                formData.append('gurus_id', this.selectedGuru)
            }
            if (this.selectedStatus === null) {
                formData.append('status', this.post.status)
            } else {
                formData.append('status', this.selectedStatus)
            }
            if (this.selectedHari === null) {
                formData.append('hari', this.post.hari)
            } else {
                formData.append('hari', this.selectedHari)
            }
            formData.append('_method', 'patch')
            await this.$axios.post('http://localhost:8000/api/jadwal/' + this.postId, formData).then((res) => {
                if (res.status === 200) {
                    this.$router.go(-1)
                } else {
                    console.log(res)
                }
                console.log(res)
            })
        },
        show() {
            console.log(this.post.id)
        }
    }
}
</script>

