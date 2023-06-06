<template>
    <section class="section">
        <div class="container">
            <div class="columns is-mobile is-centered">
                <div class="column is-full">
                    <div class="box">
                        <h1>Tambah Data Siswa</h1>
                    </div>
                </div>
            </div>

            <div class="field">
                <label class="label">Nama Siswa</label>
                <div class="control">
                    <input class="input is-info" type="text" placeholder="Text input">
                </div>
            </div>
            <div class="field">
                <label class="label">NIS</label>
                <div class="control">
                    <input class="input is-info" type="text" placeholder="Text input">
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
            <div class="field is-grouped">
                <div class="control">
                    <button class="button is-success">Submit</button>
                </div>
                <div class="control">
                    <button class="button is-light">Cancel</button>
                </div>
            </div>
        </div>
    </section>
</template>

