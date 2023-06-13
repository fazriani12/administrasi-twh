<template>
    <section class="section">
        <div class="container">
            <div class="columns is-mobile is-centered">
                <div class="column is-full">
                    <div class="box">
                        <h1>Edit Data Guru</h1>
                    </div>
                </div>
            </div>
            <form @submit="handleSubmit">
                <div class="field">
                    <label class="label">Nama Guru</label>
                    <div class="control">
                        <input class="input is-info" v-model="post.nama_guru" type="text" placeholder="Text input">
                    </div>
                </div>
                <p>{{ selectedEmail }}</p>
                <div class="field">
                    <label class="label">Email</label>
                    <div class="select is-info">
                        <select v-model.lazy="selected" @click="show">
                            <option :value="null" selected>{{ post.email }}</option>
                        </select>
                    </div>
                </div>

                <div class="field is-grouped">
                    <div class="control">
                        <button class="button is-success" type="submit">Submit</button>
                    </div>
                    <div class="control">
                        <nuxt-link to="/guru"><button class="button is-light">
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
                nama_guru: null,
                user_id: null,
                email: null
            },
            users: [],
            selectedEmail: null
        }
    },
    mounted() {
        this.$nextTick(() => {
            this.$nuxt.$loading.start()
            this.$axios.get('http://localhost:8000/api/user').then((res) => {
                this.users = res.data.data
            })
            this.$axios.get('http://localhost:8000/api/guru/' + this.postId).then((res) => {
                this.post = res.data.data[0]
            })
            this.selected = this.post.kelas_id
        })
    },
    methods: {
        async handleSubmit(event) {
            const formData = new FormData()
            event.preventDefault();
            formData.append('nama_guru', this.post.nama_guru)
            formData.append('user_id', this.post.user_id)
            formData.append('_method', 'patch')
            await this.$axios.post('http://localhost:8000/api/guru/' + this.postId, formData).then((res) => {
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
