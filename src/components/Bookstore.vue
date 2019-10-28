<template>
  <div>
    <nav
      class="navbar navbar-expand-lg navbar-light bg-light navbar-dark bg-dark row d-flex justify-content-between"
    >
      <div class="col-2">
        <img src="https://beminuscula.com/ubiqum/bookstore/img/bookstoreubi.png" class="logo" />
      </div>
      <div class="collapse navbar-collapse col-6" id="bs-example-navbar-collapse-1">
        <form class="form-inline">
          <p class="buscar">Buscar:</p>
          <input type="search" id="myInput" title="Type in a name" v-model="busqueda" />
          <!-- cuando cambia el valor del input llama a la funcion-->
          <!-- v-model="busqueda" vincula la variable busqueda al valor del input -->
        </form>
      </div>
    </nav>

    <div class="library">
      <div v-for="(book,index) in filterBooks" :key="index" class="bookstore">
        <bookUnit :bookEmpty="book"></bookUnit>
      </div>
    </div>
  </div>
</template>

<script>
import bookUnit from "./Books";
export default {
  components: { bookUnit },
  created() {
    this.cargarBooks();
  },

  data() {
    return { bookstore: [], busqueda: "" };
  },
  methods: {
    cargarBooks() {
      fetch("https://api.myjson.com/bins/1h3vb3")
        .then(response => response.json())
        .then(resp => {
          this.bookstore = resp.books;
        })
        .catch(err => console.log(err));
    }
  },
  computed: {
    filterBooks() {
      return this.bookstore.filter(
        book =>
          book.titulo.toUpperCase().includes(this.busqueda.toUpperCase()) ||
          book.descripcion.toUpperCase().includes(this.busqueda.toUpperCase())
      );
    }
  }
};
</script>

<style scoped>
.bookstore {
  background-color: transparent;
  height: 350px;
  width: 250px;
  margin-bottom: 15px;
}

.library {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  margin-top: 25px;
}

.buscar {
  font-size: 25px;
  color: azure;
  margin-right: 10px;
}

.logo {
  width: 130px;
}
</style>

