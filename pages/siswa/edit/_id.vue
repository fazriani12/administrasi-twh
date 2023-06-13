<template>
    <section class="section">
        <div class="container">
            <div class="columns is-mobile is-centered">
                <div class="column is-full">
                    <div class="box">
                        <h1>Edit Data Siswa</h1>
                    </div>
                </div>
            </div>

            <form @submit="handleSubmit">
                <div class="field">
                    <label class="label">Nama Siswa</label>
                    <div class="control">
                        <input type="text" name="" id="" v-model="post.kelas_id" hidden>
                        <input class="input is-info" v-model="post.nama_siswa" type="text" placeholder="Text input">
                    </div>
                </div>
                <div class="field">
                    <label class="label">NIS</label>
                    <div class="control">
                        <input class="input is-info" v-model="post.nis" type="text" placeholder="Text input">
                    </div>
                </div>
                <p>{{ selected }}</p>
                <div class="field">
                    <label class="label">Kelas</label>
                    <div class="select is-info">

                        <select v-model.lazy="selected" @click="show">
                            <option :value="null" selected>{{ post.nama_kelas }}</option>
                            <option v-for="(item) in kelas" :key="item.id" v-bind:value="item.id">{{ item.nama_kelas
                            }}</option>
                        </select>
                    </div>
                </div>
                <div class="field is-grouped">
                    <div class="control">
                        <button class="button is-success" type="submit">Submit</button>
                    </div>
                    <div class="control">
                        <nuxt-link to="/siswa"><button class="button is-light">
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
                nama_siswa: null,
                nis: null,
                kelas_id: null,
                nama_kelas: null
            },
            kelas: [],
            selected: null
        };
    },
    mounted() {
        this.$nextTick(() => {
            this.$nuxt.$loading.start()
            this.$axios.get('http://localhost:8000/api/kelas').then((res) => {
                this.kelas = res.data.data
            })
            this.$axios.get('http://localhost:8000/api/siswa/' + this.postId).then((res) => {
                this.post = res.data.data[0]
            })
            this.selected = this.post.kelas_id
        })
    },
    methods: {
        async handleSubmit(event) {
            const formData = new FormData()
            event.preventDefault();
            formData.append('nama_siswa', this.post.nama_siswa)
            formData.append('nis', this.post.nis)
            if (this.selected === null) {
                formData.append('kelas_id', this.post.kelas_id)
            } else {
                formData.append('kelas_id', this.selected)
            }
            formData.append('_method', 'patch')
            await this.$axios.post('http://localhost:8000/api/siswa/' + this.postId, formData).then((res) => {
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
};
</script>