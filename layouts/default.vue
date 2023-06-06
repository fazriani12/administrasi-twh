<template>
  <div>
    <nav class="navbar is-info">
      <div class="navbar-brand">
        <a class="navbar-item" href="https://bulma.io">
          <img src="~/assets/smk twh.jpg" alt="Gambar" width="28" height="28">
        </a>
        <div class="navbar-burger" data-target="navbarExampleTransparentExample">
          <span></span>
          <span></span>
          <span></span>
        </div>
      </div>

      <div id="navbarExampleTransparentExample" class="navbar-menu">
        <div class="navbar-start">
          <a class="navbar-item" href="index.vue">
            Home
          </a>
          <a class="navbar-item" href="jadwal/jadwal">
            Jadwal
          </a>
          <div class="navbar-item has-dropdown is-hoverable">
            <a class="navbar-link" href="absen/daftarabsen">
              Absen
            </a>
            <div class="navbar-dropdown is-boxed">
              <a class="navbar-item" href="absen/daftarabsen">
                Daftar Absen
              </a>
              <a class="navbar-item" href="kelas/kelas">
                Kelas
              </a>
              <a class="navbar-item" href="matapelajaran/daftarmapel">
                Matapelajaran
              </a>
            </div>
          </div>
          <a class="navbar-item" href="siswa/siswa">
            Data Siswa
          </a>
          <a class="navbar-item" href="guru/guru">
            Data guru
          </a>
        </div>

        <div class="navbar-end">
          <div class="navbar-item">
            <div class="field is-grouped">
              <p class="control">
                <a class="button is-info" href="https://github.com/jgthms/bulma/releases/download/0.9.4/bulma-0.9.4.zip">
                  <span class="icon">
                    <i class="fas fa-download is-center"></i>
                  </span>
                  <span>Logout</span>
                </a>
              </p>
            </div>
          </div>
        </div>
      </div>
    </nav>

    <section class="main-content columns">
      <div class="container column is-10">
        <Nuxt />
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data() {
    return {
      items: [
        {
          title: 'Home',
          icon: 'home',
          to: { name: 'index' },
        },
      ],
    }
  },
}
</script>
