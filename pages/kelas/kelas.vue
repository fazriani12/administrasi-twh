<template>
    <section class="section">
        <div class="container">
            <div class="columns is-mobile is-centered">
                <div class="column is-full">
                    <div class="box">
                        <h1>Daftar Nama Kelas</h1>
                    </div>
                    <div class="column">
                        <button class="button is-success is-medium">+ Tambah Data</button>
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
                        <th><abbr title="kelas_id">Kode Kelas</abbr></th>
                        <th><abbr title="nama_kelas">Nama Kelas</abbr></th>
                        <th><abbr>Tindakan</abbr></th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <th>1</th>
                        <td><a href="https://en.wikipedia.org/wiki/Leicester_City_F.C." title="X-RPL."
                                class="button is-white">X-RPL</a>
                        </td>
                        <td><button class="button is-warning">Edit</button>
                            <button class="button is-danger ">Hapus</button>
                        </td>
                    </tr>
                    <tr>
                        <th>2</th>
                        <td><a href="https://en.wikipedia.org/wiki/Leicester_City_F.C." title="X-RPL."
                                class="button is-white">XI-RPL</a>
                        </td>
                        <td><button class="button is-warning">Edit</button>
                            <button class="button is-danger ">Hapus</button>
                        </td>
                    </tr>

                </tbody>
            </table>
        </div>
    </section>
</template>


