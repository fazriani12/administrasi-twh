<template>
    <section class="section">
        <div class="container">
            <div class="columns is-mobile is-centered">
                <div class="column is-full">
                    <div class="box">
                        <h1>Edit Data Kelas</h1>
                    </div>
                </div>
            </div>
            <form @submit="handleSubmit">
                <div class="field">
                    <label class="label">Nama Kelas</label>
                    <div class="control">
                        <input class="input is-info" v-model="post.nama_kelas" type="text" placeholder="Text input">
                    </div>
                </div>
                <div class="field is-grouped">
                    <div class="control">
                        <button class="button is-success">Submit</button>
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
            postId: this.$route.params.id,
            post: {
                id: null,
                nama_kelas: null
            }
        };
    },
    mounted() {

        this.$nextTick(() => {
            this.$nuxt.$loading.start()
            this.$axios.get('http://localhost:8000/api/kelas/' + this.postId).then((res) => {
                this.post = res.data.data
            })
        })
    },
    methods: {
        async handleSubmit(event) {
            const formData = new FormData()
            event.preventDefault();
            formData.append('nama_kelas', this.post.nama_kelas)
            formData.append('_method', 'patch')
            await this.$axios.post('http://localhost:8000/api/kelas/' + this.postId, formData).then((res) => {
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
