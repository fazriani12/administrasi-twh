<template>
    <section class="section">
        <div class="container">
            <div class="columns is-mobile is-centered">
                <div class="column is-full">
                    <div class="column">
                        <nuxt-link to="/siswa/create"><button class="button is-success is-normal">
                                + Tambah Data Siswa</button></nuxt-link>
                        <nuxt-link :to="`/siswa/edit/`" class="btn btn-info mr-2"><button
                                class="button is-warning">Edit</button></nuxt-link>
                    </div>
                    <div class="column">
                        <!-- <p>{{ selectedGuru }}</p> -->
                        <P>Guru:
                        <div class="select is-info">
                            <select>
                                <option>{ item.nama_guru}</option>
                                <option>{ item.nama_guru}</option>
                            </select>
                        </div>
                        </P>
                        <P>Kelas:
                        <div class="select is-info">
                            <select>
                                <option>{ item.nama_guru}</option>
                                <option>{ item.nama_guru}</option>
                            </select>
                        </div>
                        </P>
                        <P>Nama Guru:
                        <div class="select is-info">
                            <select>
                                <option>{ item.nama_guru}</option>
                                <option>{ item.nama_guru}</option>
                            </select>
                        </div>
                        </P>
                        <P>Bulan:
                        <div class="select is-info">
                            <select>
                                <option>{ item.nama_guru}</option>
                                <option>{ item.nama_guru}</option>
                            </select>
                        </div>
                        </P>
                    </div>
                </div>
            </div>
            <table class="table is-bordered is-striped is-narrow is-hoverable is-fullwidth">
                <thead>
                    <tr>
                        <th><abbr>No</abbr></th>
                        <th>Nama</th>
                        <th><abbr title="nis">NIS</abbr></th>
                        <th>
                            <div class="field">
                                <label class="label">tgl</label>
                                <div class="select is-info">
                                    <select>
                                        <option value="1">1</option>
                                        <option value="2">2</option>
                                        <option value="3">3</option>
                                        <option value="4">4</option>
                                        <option value="5">5</option>
                                    </select>
                                </div>
                            </div>
                        </th>
                        <th><abbr title="tanggal">{tgl}</abbr></th>
                        <th><abbr title="tanggal">{tgl}</abbr></th>
                        <th><abbr title="tanggal">{tgl}</abbr></th>
                        <th><abbr title="tanggal">{tgl}</abbr></th>
                        <th><abbr title="tanggal">{tgl}</abbr></th>
                        <th><abbr title="tanggal">{tgl}</abbr></th>
                        <th><abbr title="tanggal">{tgl}</abbr></th>
                    </tr>
                </thead>
                <tfoot>
                    <tr>
                        <th><abbr title="Position">Pos</abbr></th>
                        <th>Team</th>
                        <th><abbr title="Played">Pld</abbr></th>
                        <th><abbr title="Won">W</abbr></th>
                        <th><abbr title="Drawn">D</abbr></th>
                        <th><abbr title="Lost">L</abbr></th>
                        <th><abbr title="Goals for">GF</abbr></th>
                        <th><abbr title="Goals against">GA</abbr></th>
                        <th><abbr title="Goal difference">GD</abbr></th>
                        <th><abbr title="Points">Pts</abbr></th>
                        <th>Qualification or relegation</th>
                    </tr>
                </tfoot>
                <tbody>
                    <tr>
                        <th>1</th>
                        <td><strong>Nama Siswa</strong></td>
                        <td>111111</td>
                        <td>{h}</td>
                        <td>{s}</td>
                        <td>{i}</td>
                        <td>{h}</td>
                        <td>{h}</td>
                        <td>{h}</td>
                        <td>{h}</td>
                        <td>{h}</td>
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
            absens: [],
        }
    },
    Mounted: () => {
        this.$nextTick(() => {
            this.$nuxt.$loading.start()
            this.$axios.get('http://localhost:8000/api/absen').then((res) => {
                this.absens = res.data.data
            })
        })

    },
    methods: {
        async logout() {
            await this.$auth.logout()

            this.$router.push('/login')
        },
        async hapus(id) {
            await this.$axios.delete('http://localhost:8000/api/absen/' + id).then((res) => {
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