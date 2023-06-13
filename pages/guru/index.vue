<template>
    <section class="section">
        <div class="container">
            <div class="columns is-mobile is-centered">
                <div class="column is-full">
                    <div class="box">
                        <h1>Daftar Nama Guru</h1>
                    </div>
                    <div class="column">
                        <nuxt-link to="/guru/create"><button class="button is-success is-medium">
                                + Tambah Data</button></nuxt-link>
                    </div>
                    <div class="field has-addons">
                        <div class="control">
                            <input class="input" type="text" placeholder="Find a repository">
                        </div>
                        <div class="control">
                            <a class="button is-info">
                                Search
                            </a>
                        </div>
                    </div>
                </div>
            </div>

            <table class="table">
                <thead>
                    <tr>
                        <th><abbr title="gurus_id">No</abbr></th>
                        <th><abbr title="nama_guru">Nama</abbr></th>
                        <th><abbr title="email">Email</abbr></th>
                        <th><abbr>Action</abbr></th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(item, index) in gurus" :key="item.id">
                        <th>{{ index + 1 }}</th>
                        <td>{{ item.nama_guru }}</td>
                        <td>{{ item.email }}</td>
                        <td><nuxt-link :to="`/guru/edit/${item.id}`" class="btn btn-info mr-2"><button
                                    class="button is-warning">Edit</button></nuxt-link>
                            <button @click="hapus(item.id)" class="button is-danger ">Hapus</button>
                        </td>
                    </tr>
                </tbody>
            </table>

        </div>
    </section>
</template>

<script>
export default {
    data() {
        return {
            user: this.$auth.user,
            gurus: [],
        }
    },
    mounted() {
        this.$nextTick(() => {
            this.$nuxt.$loading.start()
            this.$axios.get('http://localhost:8000/api/guru').then((res) => {
                this.gurus = res.data.data
            })
        })
    },
    methods: {
        async logout() {
            await this.$auth.logout()

            this.$router.push('/login')
        },
        async hapus(id) {
            await this.$axios.delete('http://localhost:8000/api/guru/' + id).then((res) => {
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