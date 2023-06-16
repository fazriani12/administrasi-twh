<template>
    <div>
        <div class="box">
            <div class="nama-guru-column">
                <h3>Nama Guru: {{ namaGuru }}</h3>
                <p></p>
            </div>

            <div class="nama-matapelajaran-column">
                <h3>Nama Mata Pelajaran: {{ namaMatapelajaran }}</h3>
            </div>
            <div class="tahun-column">
                <h3>Bulan/Tahun: {{ bulan }}/{{ tahun }}</h3>
            </div>
        </div>
        <div class="box">
            <b-table :data="data" :columns="columnsTabel" :paginated="isPaginated" :per-page="perPage"></b-table>
        </div>
        <div class=" box pokokBahasan-column">
            <h3>Pokok Bahasan: {{ pokokBahasan }}</h3>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            isPaginated: true,
            perPage: 5,
            data: [],
            columnsTabel: [
                {
                    field: 'nama_siswa',
                    label: 'Nama Siswa',
                    searchable: true,
                },
                {
                    field: 'nis',
                    label: 'NIS',
                },
                {
                    field: 'nama_kelas',
                    label: 'Kelas',
                },
                {
                    field: 'nama_matapelajaran',
                    label: 'Mapel',
                },
                {
                    field: 'tanggal',
                    label: 'Tanggal',
                    centered: true,
                },
                {
                    field: 'absensi',
                    label: 'Kehadiran',
                }
            ],
            namaGuru: '',
            namaMatapelajaran: '',
            tahun: '',
            bulan: '',
            pokokBahasan: ''
        };
    },
    mounted() {
        this.$nextTick(() => {
            this.$nuxt.$loading.start();
            this.$axios
                .get('http://localhost:8000/api/absen')
                .then((res) => {
                    this.data = res.data.data;
                    this.namaGuru = this.data[0].nama_guru; // Mengambil nama guru dari data pertama
                    this.namaMatapelajaran = this.data[0].nama_matapelajaran; // Mengambil nama mata pelajaran dari data pertama
                    this.tahun = this.data[0].tahun;
                    this.bulan = this.data[0].bulan;
                    this.pokokBahasan = this.data[0].pokok_bahasan;
                    this.$nuxt.$loading.finish();
                })
                .catch((error) => {
                    console.error(error);
                    this.$nuxt.$loading.fail();
                });
        });
    },
};
</script>
