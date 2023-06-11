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

                <div class="field">
                    <label class="label">Kelas</label>
                    <div class="select is-info">
                        <select>
                            <option value="X-TP">X-TP</option>
                            <option value="X-RPL">X-RPL</option>
                            <option value="X-TKR">X-TKR</option>
                            <option value="XI-RPL">XI-RPL</option>
                            <option value="XI-TKR">XI-TKR</option>
                            <option value="XI-TP">XI-TP</option>
                            <option value="XII-RPL">XII-RPL</option>
                            <option value="XII-TKR">XII-TKR</option>
                            <option value="XII-TP">XII-TP</option>
                        </select>
                    </div>
                </div>

                <div class="field">
                    <label class="label">Nama Guru</label>
                    <div class="control">
                        <input class="input is-info" v-model="post.nama_guru" type="text" placeholder="Text input">
                    </div>
                </div>

                <div class="field">
                    <label class="label">Status Matapelajaran</label>
                    <div class="select is-info">
                        <select>
                            <option value="Produktif">Produktif</option>
                            <option value="Non Produktif">Non Produktif</option>
                        </select>
                    </div>
                </div>

                <div class="field is-grouped">
                    <div class="control">
                        <button class="button is-success" type="submit">Submit</button>
                    </div>
                    <div class="control">
                        <nuxt-link to="/kelas"><button class="button is-light">
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
                nama_kelas: null,
                nama_guru: null,
                status: null,


            }
        };
    },
    methods: {
        async handleSubmit(event) {
            const formData = new FormData()
            event.preventDefault();
            formData.append('nama_matapelajaran', this.post.nama_matapelajaran)
            formData.append('nama_kelas', this.post.nama_kelas)
            formData.append('nama_guru', this.post.nama_guru)
            formData.append('status', this.post.status)
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

