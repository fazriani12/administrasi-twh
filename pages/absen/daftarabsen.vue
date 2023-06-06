<template>
    <section class="section">
        <div class="container">
            <div class="columns is-mobile is-centered">
                <div class="column is-full">
                    <div class="box">
                        <h1>Data Absen</h1>
                    </div>
                    <div class="column">
                        <button class="button is-success is-medium">+ Tambah Absen</button>
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
                        <th><abbr title="nama_kelas">Nama Kelas</abbr></th>
                        <th><abbr title="matapelajarans_id">Nama Matapelajaran</abbr></th>
                        <th><abbr>Tindakan</abbr></th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>X-RPL</td>
                        <th><a href="absen/absenmapel" title="X-RPL." class="button is-white">Mapel1</a></th>
                        <td>
                            <button class="button is-info" href="absen/absenmapel">Absen</button>
                            <button class="button is-warning">Edit</button>
                            <button class="button is-danger ">Hapus</button>
                        </td>
                    </tr>
                    <tr>
                        <td>X-RPL</td>
                        <th><a href="absen/absenmapel" title="X-RPL." class="button is-white">Mapel2</a></th>
                        <td>
                            <button class="button is-info">Absen</button>
                            <button class="button is-warning">Edit</button>
                            <button class="button is-danger ">Hapus</button>
                        </td>
                    </tr>

                </tbody>
            </table>
        </div>
    </section>
</template>


