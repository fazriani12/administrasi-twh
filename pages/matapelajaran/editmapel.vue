<template>
    <section class="section">
        <div class="container">
            <div class="columns is-mobile is-centered">
                <div class="column is-full">
                    <div class="box">
                        <h1>Edit Data Matapelajaran</h1>
                    </div>
                </div>
            </div>

            <div class="field">
                <label class="label">Nama Matapelajaran</label>
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

            <div class="field">
                <label class="label">Hari</label>
                <div class="select is-info">
                    <select>
                        <option value="Senin">Senin</option>
                        <option value="Selasa">Selasa</option>
                        <option value="Rabu">Rabu</option>
                        <option value="Kamis">Kamis</option>
                        <option value="Jumat">Jumat</option>
                    </select>
                </div>
            </div>

            <div class="field">
                <div class="control">
                    <label class="label">Jam Awal</label>
                    <div class="control">
                        <input class="input is-info" type="time" id="timeInput">
                    </div>
                </div>
            </div>

            <div class="field">
                <div class="control">
                    <label class="label">Jam Akhir</label>
                    <div class="control">
                        <input class="input is-info" type="time" id="timeInput">
                    </div>
                </div>
            </div>

            <div class="field">
                <label class="label">Jumlah Jam</label>
                <div class="control">
                    <input class="input is-info" type="text" placeholder="Text input">
                </div>
            </div>

            <div class="field">
                <label class="label">Nama Guru</label>
                <div class="control">
                    <input class="input is-info" type="text" placeholder="Text input">
                </div>
            </div>

            <div class="field">
                <label class="label">Status Matapelajaran</label>
                <div class="select is-info">
                    <select>
                        <option value="Produktif">Produktif</option>
                        <option value="Non Produktif">Non Produktif</option>
                    </select>
                </div>
            </div>

            <div class="field is-grouped">
                <div class="control">
                    <button class="button is-success">Submit</button>
                </div>
                <div class="control">
                    <button class="button is-link is-light">Cancel</button>
                </div>
            </div>

        </div>
    </section>
</template>

