<template>
    <section class="section">
        <div class="container">
            <div class="columns is-mobile is-centered">
                <div class="column is-full">
                    <div class="box">
                        <h1>Tambah Data Kelas</h1>
                    </div>
                </div>
            </div>

            <form @submit="handleSubmit">
                <div class="field">
                    <label class="label">Nama Kelas</label>
                    <div class="control">
                        <input class="input is-info" type="text" v-model="post.nama_kelas" placeholder="Text input">
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
                nama_kelas: null
            }
        };
    },
    methods: {
        async handleSubmit(event) {
            const formData = new FormData()
            event.preventDefault();
            formData.append('nama_kelas', this.post.nama_kelas)
            await this.$axios.post('http://localhost:8000/api/kelas', formData).then((res) => {
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
