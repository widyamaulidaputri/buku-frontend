<template>
  <div class="container">
    <h1>Members</h1>
    <form @submit.prevent="getAnggota">
      <div class="form-group">
        <label for="nomor">Nomor Anggota:</label>
        <input type="text" class="form-control" id="nomor" v-model="nomor" required>
      </div>
      <button type="submit" class="btn btn-primary">Cari Anggota</button>
    </form>

    <hr>

    <h2>Tambah Anggota</h2>
    <form @submit.prevent="insertAnggota">
      <div class="form-group">
        <label for="nomorInsert">Nomor Anggota:</label>
        <input type="text" class="form-control" id="nomorInsert" v-model="nomorInsert" required>
      </div>
      <div class="form-group">
        <label for="namaInsert">Nama:</label>
        <input type="text" class="form-control" id="namaInsert" v-model="namaInsert" required>
      </div>
      <div class="form-group">
        <label for="jenisKelaminInsert">Jenis Kelamin:</label>
        <input type="text" class="form-control" id="jenisKelaminInsert" v-model="jenisKelaminInsert" required>
      </div>
      <div class="form-group">
        <label for="alamatInsert">Alamat:</label>
        <input type="text" class="form-control" id="alamatInsert" v-model="alamatInsert" required>
      </div>
      <div class="form-group">
        <label for="noHpInsert">No. HP:</label>
        <input type="text" class="form-control" id="noHpInsert" v-model="noHpInsert" required>
      </div>
      <div class="form-group">
        <label for="tanggalTerdaftarInsert">Tanggal Terdaftar:</label>
        <input type="text" class="form-control" id="tanggalTerdaftarInsert" v-model="tanggalTerdaftarInsert" required>
      </div>
      <button type="submit" class="btn btn-primary">Tambah Anggota</button>
    </form>

    <hr>

    <h2>Edit Anggota</h2>
    <form @submit.prevent="updateAnggota">
      <div class="form-group">
        <label for="nomorUpdate">Nomor Anggota:</label>
        <input type="text" class="form-control" id="nomorUpdate" v-model="nomorUpdate" required>
      </div>
      <div class="form-group">
        <label for="namaUpdate">Nama:</label>
        <input type="text" class="form-control" id="namaUpdate" v-model="namaUpdate" required>
      </div>
      <div class="form-group">
        <label for="jenisKelaminUpdate">Jenis Kelamin:</label>
        <input type="text" class="form-control" id="jenisKelaminUpdate" v-model="jenisKelaminUpdate" required>
      </div>
      <div class="form-group">
        <label for="alamatUpdate">Alamat:</label>
        <input type="text" class="form-control" id="alamatUpdate" v-model="alamatUpdate" required>
      </div>
      <div class="form-group">
        <label for="noHpUpdate">No. HP:</label>
        <input type="text" class="form-control" id="noHpUpdate" v-model="noHpUpdate" required>
      </div>
      <div class="form-group">
        <label for="tanggalTerdaftarUpdate">Tanggal Terdaftar:</label>
        <input type="text" class="form-control" id="tanggalTerdaftarUpdate" v-model="tanggalTerdaftarUpdate" required>
      </div>
      <button type="submit" class="btn btn-primary">Update Anggota</button>
    </form>

    <hr>

    <h2>Hapus Anggota</h2>
    <form @submit.prevent="deleteAnggota">
      <div class="form-group">
        <label for="nomorDelete">Nomor Anggota:</label>
        <input type="text" class="form-control" id="nomorDelete" v-model="nomorDelete" required>
      </div>
      <button type="submit" class="btn btn-danger">Hapus Anggota</button>
    </form>

    <hr>

    <h2>Seluruh Anggota</h2>
    <table class="table">
      <thead>
      <tr>
        <th>ID</th>
        <th>Nomor</th>
        <th>Nama</th>
        <th>Jenis Kelamin</th>
        <th>Alamat</th>
        <th>No. HP</th>
        <th>Tanggal Terdaftar</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="anggota in anggotaList" :key="anggota.id">
        <td>{{ anggota.id }}</td>
        <td>{{ anggota.nomor }}</td>
        <td>{{ anggota.nama }}</td>
        <td>{{ anggota.jenis_kelamin }}</td>
        <td>{{ anggota.alamat }}</td>
        <td>{{ anggota.no_hp }}</td>
        <td>{{ anggota.tanggal_terdaftar }}</td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      nomor: '',
      nomorInsert: '',
      namaInsert: '',
      jenisKelaminInsert: '',
      alamatInsert: '',
      noHpInsert: '',
      tanggalTerdaftarInsert: '',
      nomorUpdate: '',
      namaUpdate: '',
      jenisKelaminUpdate: '',
      alamatUpdate: '',
      noHpUpdate: '',
      tanggalTerdaftarUpdate: '',
      nomorDelete: '',
      anggotaList: [],
    }
  },
  methods: {
    getAnggota() {
      axios.get(`http://localhost/buku/selectanggotabynomor.php${this.nomor}`)
          .then(response => {
            this.anggotaList = [response.data]
          })
          .catch(error => {
            console.error(error)
          })
    },
    insertAnggota() {
      const newAnggota = {
        nomor: this.nomorInsert,
        nama: this.namaInsert,
        jenis_kelamin: this.jenisKelaminInsert,
        alamat: this.alamatInsert,
        no_hp: this.noHpInsert,
        tanggal_terdaftar: this.tanggalTerdaftarInsert,
      }

      axios.post('http://localhost/buku/insertanggota.php', newAnggota)
          .then(response => {
            this.clearInsertForm()
            this.getAnggotaList()
          })
          .catch(error => {
            console.error(error)
          })
    },
    updateAnggota() {
      const updatedAnggota = {
        nomor: this.nomorUpdate,
        nama: this.namaUpdate,
        jenis_kelamin: this.jenisKelaminUpdate,
        alamat: this.alamatUpdate,
        no_hp: this.noHpUpdate,
        tanggal_terdaftar: this.tanggalTerdaftarUpdate,
      }

      axios.put(`http://localhost/buku/updateanggota.php${this.nomorUpdate}`, updatedAnggota)
          .then(response => {
            this.clearUpdateForm()
            this.getAnggotaList()
          })
          .catch(error => {
            console.error(error)
          })
    },
    deleteAnggota() {
      axios.delete(`http://localhost/buku/deleteanggota.php${this.nomorDelete}`)
          .then(response => {
            this.clearDeleteForm()
            this.getAnggotaList()
          })
          .catch(error => {
            console.error(error)
          })
    },
    getAnggotaList() {
      axios.get('http://localhost/buku/selectanggota.php')
          .then(response => {
            this.anggotaList = response.data
          })
          .catch(error => {
            console.error(error)
          })
    },
    clearInsertForm() {
      this.nomorInsert = ''
      this.namaInsert = ''
      this.jenisKelaminInsert = ''
      this.alamatInsert = ''
      this.noHpInsert = ''
      this.tanggalTerdaftarInsert = ''
    },
    clearUpdateForm() {
      this.nomorUpdate = ''
      this.namaUpdate = ''
      this.jenisKelaminUpdate = ''
      this.alamatUpdate = ''
      this.noHpUpdate = ''
      this.tanggalTerdaftarUpdate = ''
    },
    clearDeleteForm() {
      this.nomorDelete = ''
    },
  },
  mounted() {
    this.getAnggotaList()
  },
}
</script>

<style>
.container {
  margin-top: 20px;
}
</style>
