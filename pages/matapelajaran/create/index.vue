<template>
    <section class="section">
        <div class="container">
            <div class="columns is-mobile is-centered">
                <div class="column is-full">
                    <div class="box">
                        <h1>Tambah Data Matapelajaran</h1>
                    </div>
                </div>
            </div>
            <form @submit="handleSubmit">
                <div class="field">
                    <label class="label">Nama Matapelajaran</label>
                    <div class="control">
                        <input class="input is-info" v-model="post.nama_matapelajaran" type="text" placeholder="Text input">
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
                    <label class="label">Status Matapelajaran</label>
                    <div class="select is-info">
                        <select v-model="selectedStatus">
                            <option value="Produktif">Produktif</option>
                            <option value="Nonproduktif">Nonproduktif</option>
                        </select>
                    </div>
                </div>

                <div class="field is-grouped">
                    <div class="control">
                        <button class="button is-success" type="submit">Submit</button>
                    </div>
                    <div class="control">
                        <nuxt-link to="/matapelajaran"><button class="button is-light">
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
                nama_matapelajaran: null,
                kelas_id: null,
                gurus_id: null,
                status: null

            },
            kelas: [],
            selectedKelas: null,
            guru: [],
            selectedGuru: null,
            selectedStatus: null

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
        })
    },
    methods: {
        async handleSubmit(event) {
            const formData = new FormData()
            event.preventDefault();
            formData.append('nama_matapelajaran', this.post.nama_matapelajaran)
            formData.append('kelas_id', this.selectedKelas)
            formData.append('gurus_id', this.selectedGuru)
            formData.append('status', this.selectedStatus)
            await this.$axios.post('http://localhost:8000/api/matapelajaran', formData).then((res) => {
                if (res.status === 200) {
                    this.$router.go(-1)
                } else {
                    console.log(res)
                }
                console.log(res)
            })
        }
    }
};
</script>

