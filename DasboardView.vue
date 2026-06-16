<template>
  <div>
    <!-- Header -->
    <header class="header">
      <h1>Dashboard Aplikasi SITTA</h1>

      <nav>
        <ul class="nav-menu">
          <li>
            <RouterLink to="/dashboard" class="active">
              Beranda
            </RouterLink>
          </li>

          <li>
            <RouterLink to="/stok">
              Informasi Bahan Ajar
            </RouterLink>
          </li>

          <li>
            <RouterLink to="/tracking">
              Tracking Pengiriman
            </RouterLink>
          </li>

          <li class="dropdown">
            <button class="dropbtn">
              Laporan ▼
            </button>

            <div class="dropdown-content">
              <a href="#monitoring">Monitoring Progress DO Bahan Ajar</a>
              <a href="#rekap">Rekap Bahan Ajar</a>
              <a href="#histori">Histori Transaksi Bahan Ajar</a>
            </div>
          </li>

          <li>
            <button
              class="logout-button"
              @click="logout"
            >
              Keluar
            </button>
          </li>
        </ul>
      </nav>
    </header>

    <!-- Main Content -->
    <main class="container">
      <section class="greeting">
        <h2>{{ greetingMessage }}</h2>
        <p>
          Anda login sebagai
          <span>{{ userInfo }}</span>.
        </p>
      </section>

      <section class="quick-links">
        <h3>Menu Cepat</h3>

        <div class="link-grid">
          <RouterLink
            to="/stok"
            class="card-link"
          >
            Informasi Bahan Ajar
          </RouterLink>

          <RouterLink
            to="/tracking"
            class="card-link"
          >
            Tracking Pengiriman
          </RouterLink>

          <a
            href="#monitoring"
            class="card-link"
          >
            Monitoring DO
          </a>
        </div>
      </section>

      <section
        id="monitoring"
        class="report-section"
      >
        <h3>Monitoring Progress DO Bahan Ajar</h3>
        <p>
          Konten untuk Monitoring Progress Delivery Order akan ditampilkan di sini.
        </p>
      </section>

      <section
        id="rekap"
        class="report-section"
      >
        <h3>Rekap Bahan Ajar</h3>
        <p>
          Konten untuk Rekapitulasi Bahan Ajar akan ditampilkan di sini.
        </p>
      </section>

      <section
        id="histori"
        class="report-section"
      >
        <h3>Histori Transaksi Bahan Ajar</h3>
        <p>
          Konten untuk Histori Transaksi Bahan Ajar akan ditampilkan di sini.
        </p>
      </section>
    </main>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

const greetingMessage = ref('Selamat Datang!')
const userInfo = ref('Pengguna SITTA')

onMounted(() => {
  const namaUser = localStorage.getItem('namaUser')

  if (namaUser) {
    userInfo.value = namaUser
    greetingMessage.value = `Selamat Datang, ${namaUser}!`
  }
})

const logout = () => {
  localStorage.removeItem('namaUser')
  router.push('/')
}
</script>