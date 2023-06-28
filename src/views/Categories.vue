<template>
  <div class="container">
    <h1>Book Categories</h1>
    <div class="mb-3">
      <button class="btn btn-primary" @click="showAddModal">Tambah Kategori</button>
    </div>
    <table class="table">
      <thead>
      <tr>
        <th>ID</th>
        <th>Kode</th>
        <th>Kategori</th>
        <th>Aksi</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="kategori in kategoris" :key="kategori.id">
        <td>{{ kategori.id }}</td>
        <td>{{ kategori.kode }}</td>
        <td>{{ kategori.kategori }}</td>
        <td>
          <button class="btn btn-primary btn-sm" @click="showEditModal(kategori)">Edit</button>
          <button class="btn btn-danger btn-sm" @click="deleteKategori(kategori.kode)">Hapus</button>
        </td>
      </tr>
      </tbody>
    </table>
    <!-- Modal Tambah/Edit Kategori -->
    <div class="modal" :class="{ 'show': showModal }">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">{{ modalTitle }}</h5>
            <button type="button" class="btn-close" aria-label="Close" @click="hideModal"></button>
          </div>
          <div class="modal-body">
            <form @submit.prevent="submitForm">
              <div class="mb-3">
                <label for="kode" class="form-label">Kode</label>
                <input type="text" class="form-control" id="kode" v-model="form.kode" required>
              </div>
              <div class="mb-3">
                <label for="kategori" class="form-label">Kategori</label>
                <input type="text" class="form-control" id="kategori" v-model="form.kategori" required>
              </div>
              <button type="submit" class="btn btn-primary">Simpan</button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      kategoris: [],
      showModal: false,
      modalTitle: '',
      form: {
        id: null,
        kode: '',
        kategori: '',
      },
    };
  },
  mounted() {
    this.fetchKategoris();
  },
  methods: {
    fetchKategoris() {
      axios.get('http://localhost/buku/selectkategori.php')
          .then((response) => {
            this.kategoris = response.data;
          })
          .catch((error) => {
            console.log(error);
          });
    },
    showAddModal() {
      this.modalTitle = 'Tambah Kategori';
      this.form = {
        id: null,
        kode: '',
        kategori: '',
      };
      this.showModal = true;
    },
    showEditModal(kategori) {
      this.modalTitle = 'Edit Kategori';
      this.form = {
        id: kategori.id,
        kode: kategori.kode,
        kategori: kategori.kategori,
      };
      this.showModal = true;
    },
    hideModal() {
      this.showModal = false;
    },
    submitForm() {
      if (this.form.id) {
        // Memanggil API untuk update kategori
        axios.put(`http://localhost/buku/updatekategoribykode.php${this.form.id}`, this.form)
            .then(() => {
              this.hideModal();
              this.fetchKategoris();
            })
            .catch((error) => {
              console.log(error);
            });
      } else {
        // Memanggil API untuk insert kategori baru
        axios.post('http://localhost/buku/insertkategori.php', this.form)
            .then(() => {
              this.hideModal();
              this.fetchKategoris();
            })
            .catch((error) => {
              console.log(error);
            });
      }
    },
    deleteKategori(kode) {
      if (confirm('Anda yakin ingin menghapus kategori ini?')) {
        // Memanggil API untuk delete kategori
        axios.delete(`http://localhost/buku/deletekategoribykode.php/${kode}`)
            .then(() => {
              this.fetchKategoris();
            })
            .catch((error) => {
              console.log(error);
            });
      }
    },
  },
};
</script>

<style scoped>
/* Gaya khusus komponen ini */
</style>
