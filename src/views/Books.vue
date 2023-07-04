<template>
  <div class="container">
    <h1>Book Store</h1>
    <div class="row">
      <div class="col-md-4">
        <form @submit.prevent="getBook">
          <div class="form-group">
            <img src="../assets/book.jpg" class="img-fluid">


          </div>
          <button type="submit" class="btn btn-primary">Search</button>
        </form>
      </div>
      <div class="col-md-6">
        <form @submit.prevent="addBook">
          <div class="form-group">
            <label for="bookCodeAdd">Kode Buku:</label>
            <input type="text" class="form-control" v-model="bookCodeAdd" id="bookCodeAdd" required>
          </div>
          <div class="form-group">
            <label for="bookCategoryCode">Kode Kategori:</label>
            <input type="text" class="form-control" v-model="bookCategoryCode" id="bookCategoryCode" required>
          </div>
          <div class="form-group">
            <label for="bookTitle">Judul:</label>
            <input type="text" class="form-control" v-model="bookTitle" id="bookTitle" required>
          </div>
          <div class="form-group">
            <label for="bookAuthor">Pengarang:</label>
            <input type="text" class="form-control" v-model="bookAuthor" id="bookAuthor" required>
          </div>
          <div class="form-group">
            <label for="bookPublisher">Penerbit:</label>
            <input type="text" class="form-control" v-model="bookPublisher" id="bookPublisher" required>
          </div>
          <div class="form-group">
            <label for="bookYear">Tahun:</label>
            <input type="text" class="form-control" v-model="bookYear" id="bookYear" required>
          </div>
          <div class="form-group">
            <label for="bookInputDate">Tanggal Input:</label>
            <input type="date" class="form-control" v-model="bookInputDate" id="bookInputDate" required>
          </div>
          <div class="form-group">
            <label for="bookPrice">Harga:</label>
            <input type="text" class="form-control" v-model="bookPrice" id="bookPrice" required>
          </div>
          <div class="form-group">
            <label for="bookCover">File Cover:</label>
            <input type="file" class="form-control-file" id="bookCover" @change="handleFileUpload">
          </div>
          <button type="submit" class="btn btn-primary">Tambah</button>
        </form>
      </div>
    </div>
    <hr>
    <table class="table">
      <thead>
      <tr>
        <th>ID</th>
        <th>Kode</th>
        <th>Kode Kategori</th>
        <th>Judul</th>
        <th>Pengarang</th>
        <th>Penerbit</th>
        <th>Tahun</th>
        <th>Tanggal Input</th>
        <th>Harga</th>
        <th>File Cover</th>
        <th>Aksi</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="book in books" :key="book.id">
        <td>{{ book.id }}</td>
        <td>{{ book.kode }}</td>
        <td>{{ book.kode_kategori }}</td>
        <td>{{ book.judul }}</td>
        <td>{{ book.pengarang }}</td>
        <td>{{ book.penerbit }}</td>
        <td>{{ book.tahun }}</td>
        <td>{{ book.tanggal_input }}</td>
        <td>{{ book.harga }}</td>
        <td>{{ book.file_cover }}</td>
        <td>
          <button class="btn btn-sm btn-primary" @click="editBook(book)">Edit</button>
          <button class="btn btn-sm btn-danger" @click="deleteBook(book)">Delete</button>
        </td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      books: [],
      bookCode: '',
      bookCodeAdd: '',
      bookCategoryCode: '',
      bookTitle: '',
      bookAuthor: '',
      bookPublisher: '',
      bookYear: '',
      bookInputDate: '',
      bookPrice: '',
      bookCover: null,
    };
  },
  mounted() {
    this.getBooks();
  },
  methods: {
    getBooks() {
      axios.get('http://localhost/buku/selectbuku.php')
          .then(response => {
            this.books = response.data;
          })
          .catch(error => {
            console.log(error);
          });
    },
    getBook() {
      if (this.bookCode !== '') {
        axios.get('http://localhost/buku/selectbukubykode.php' + this.bookCode)
            .then(response => {
              this.books = [response.data];
            })
            .catch(error => {
              console.log(error);
            });
      } else {
        this.getBooks();
      }
    },
    addBook() {
      const formData = new FormData();
      formData.append('kode', this.bookCodeAdd);
      formData.append('kode_kategori', this.bookCategoryCode);
      formData.append('judul', this.bookTitle);
      formData.append('pengarang', this.bookAuthor);
      formData.append('penerbit', this.bookPublisher);
      formData.append('tahun', this.bookYear);
      formData.append('tanggal_input', this.bookInputDate);
      formData.append('harga', this.bookPrice);
      formData.append('file_cover', this.bookCover);

      axios.post('https://buku--widyamaulidaput.repl.co/insertbuku.php',)
          .then(response => {
            this.getBooks();
            this.resetForm();
          })
          .catch(error => {
            console.log(error);
          });
    },
    editBook(book) {
      // Implement logic for editing a book
      this.$http.post('/api/books', )
          .then(response => {
            this.getBooks();
            this.resetForm();
          })
          .catch(error => {
            console.log(error);
          });
    },
    deleteBook(book) {
      // Implement logic for deleting a book
      axios.delete('https://buku--widyamaulidaput.repl.co/deletebukubykode.php', )
          .then(response => {
            this.getBooks();
            this.resetForm();
          })
          .catch(error => {
            console.log(error);
          });
    },
    handleFileUpload(event) {
      this.bookCover = event.target.files[0];
    },
    resetForm() {
      this.bookCodeAdd = '';
      this.bookCategoryCode = '';
      this.bookTitle = '';
      this.bookAuthor = '';
      this.bookPublisher = '';
      this.bookYear = '';
      this.bookInputDate = '';
      this.bookPrice = '';
      this.bookCover = null;
    }
  }
};
</script>

<style>
.container {
  margin-top: 20px;
}
</style>
