<template>
  <div>
    <!-- Header -->
    <header class="header">
      <h1>Informasi Bahan Ajar</h1>

      <nav>
        <ul class="nav-menu">
          <li>
            <RouterLink to="/dashboard">
              Beranda
            </RouterLink>
          </li>

          <li>
            <RouterLink
              to="/stok"
              class="active"
            >
              Informasi Bahan Ajar
            </RouterLink>
          </li>

          <li>
            <RouterLink to="/tracking">
              Tracking Pengiriman
            </RouterLink>
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

    <main class="container">
      <h2>Paragaan Data Bahan Ajar</h2>

      <button
        class="primary-button"
        @click="showForm = true"
      >
        Tambah Stok Baru
      </button>

      <!-- Form Tambah -->
      <section
        v-if="showForm"
        style="margin-top:20px"
      >
        <h3>Input Bahan Ajar Baru</h3>

        <form
          class="stock-form"
          @submit.prevent="saveStock"
        >
          <input
            v-model="newStock.kodeLokasi"
            type="text"
            placeholder="Kode Lokasi"
            required
          />

          <input
            v-model="newStock.kodeBarang"
            type="text"
            placeholder="Kode Barang (ASIP4301)"
            required
          />

          <input
            v-model="newStock.namaBarang"
            type="text"
            placeholder="Nama Barang"
            required
          />

          <input
            v-model="newStock.jenisBarang"
            type="text"
            placeholder="Jenis Barang (BMP)"
            required
          />

          <input
            v-model="newStock.edisi"
            type="text"
            placeholder="Edisi"
            required
          />

          <input
            v-model.number="newStock.stok"
            type="number"
            min="1"
            placeholder="Stok"
            required
          />

          <input
            v-model="newStock.cover"
            type="text"
            placeholder="URL Cover Buku"
          />

          <button
            type="submit"
            class="success-button"
          >
            Simpan Stok
          </button>

          <button
            type="button"
            class="secondary-button"
            @click="cancelAdd"
          >
            Batal
          </button>
        </form>
      </section>

      <!-- Tabel -->
      <div
        class="table-container"
        style="margin-top:20px"
      >
        <table>
          <thead>
            <tr>
              <th>Cover</th>
              <th>Kode Lokasi</th>
              <th>Kode Barang</th>
              <th>Nama Barang</th>
              <th>Jenis</th>
              <th>Edisi</th>
              <th>Stok</th>
              <th>Aksi</th>
            </tr>
          </thead>

          <tbody>
            <tr
              v-for="(item,index) in stokList"
              :key="index"
            >
              <td>
                <img
                  :src="item.cover || defaultCover"
                  alt="cover"
                  width="60"
                />
              </td>

              <td>{{ item.kodeLokasi }}</td>
              <td>{{ item.kodeBarang }}</td>
              <td>{{ item.namaBarang }}</td>
              <td>{{ item.jenisBarang }}</td>
              <td>{{ item.edisi }}</td>
              <td>{{ item.stok }}</td>

              <td>
                <button
                  class="secondary-button"
                  @click="editStock(index)"
                >
                  Edit
                </button>

                <button
                  class="logout-button"
                  @click="deleteStock(index)"
                >
                  Hapus
                </button>
              </td>
            </tr>

            <tr v-if="stokList.length === 0">
              <td
                colspan="8"
                style="text-align:center"
              >
                Data stok belum tersedia
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </main>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

const defaultCover =
  'https://via.placeholder.com/60x80?text=Buku'

const showForm = ref(false)

const stokList = ref([])

const newStock = ref({
  kodeLokasi: '',
  kodeBarang: '',
  namaBarang: '',
  jenisBarang: '',
  edisi: '',
  stok: 0,
  cover: ''
})

onMounted(() => {
  const savedData = localStorage.getItem('stokList')

  if (savedData) {
    stokList.value = JSON.parse(savedData)
  }
})

function saveStock() {
  stokList.value.push({
    ...newStock.value
  })

  localStorage.setItem(
    'stokList',
    JSON.stringify(stokList.value)
  )

  resetForm()
}

function resetForm() {
  newStock.value = {
    kodeLokasi: '',
    kodeBarang: '',
    namaBarang: '',
    jenisBarang: '',
    edisi: '',
    stok: 0,
    cover: ''
  }

  showForm.value = false
}

function cancelAdd() {
  resetForm()
}

function deleteStock(index) {
  if (confirm('Hapus data ini?')) {
    stokList.value.splice(index, 1)

    localStorage.setItem(
      'stokList',
      JSON.stringify(stokList.value)
    )
  }
}

function editStock(index) {
  const data = stokList.value[index]

  newStock.value = { ...data }

  stokList.value.splice(index, 1)

  localStorage.setItem(
    'stokList',
    JSON.stringify(stokList.value)
  )

  showForm.value = true
}

function logout() {
  localStorage.removeItem('namaUser')
  router.push('/')
}
</script>