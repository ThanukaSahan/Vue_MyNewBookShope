<template>
  <h1>Select Your Books you wish to purchase</h1>

  <div class="bodyDiv">
    <div class="filters">
      <button type="button" class="btn btn-success" @click="onPurchase">
        <font-awesome-icon :icon="['fas', 'cart-shopping']" />
        buy {{ noOfSelectBooks }}
      </button>
      <div class="mainFilter">
        <label>Filter By</label>
        <select @change="onFilterOptionChange($event)">
          <option value="1">Default</option>
          <option value="2">Price : Low to High</option>
          <option value="3">Price : High to Low</option>
          <option value="4">By Book</option>
          <option value="5">By Author</option>
          <option value="6">By Category</option>
        </select>
      </div>
      <div v-if="isBookName">
        <label>Enter Name of the book</label>
        <input type="text" @keyup="SearchBookByName($event)" />
      </div>
      <div v-if="isBookAuthor">
        <label>Enter Author Name</label>
        <input type="text" @keyup="SearchBookByAuthor($event)" />
      </div>
      <div v-if="isCategory">
        <label>category</label>
        <select
          v-model="selected"
          id="bookcat"
          @change="onChangeCategory($event)"
        >
          <option value="">--select category--</option>
          <option
            v-for="category in bookCategorys"
            :key="category.id"
            v-bind:value="category.category"
          >
            {{ category.category }}
          </option>
        </select>
      </div>
    </div>
    <div>
      <table>
        <tr>
          <th></th>
          <th>Name of the Book</th>
          <th>Book Author</th>
          <th>category</th>
          <th>language</th>
          <th>Price $</th>
        </tr>
        <tr v-for="book in books" :key="book.id">
          <td class="col-sm col-1">
            <input
              type="checkbox"
              v-model="book.isItemSelected"
              @change="onSelectBook(book)"
            />
          </td>
          <td class="col-sm col-3">{{ book.bookname }}</td>
          <td class="col-sm col-3">{{ book.author }}</td>
          <td class="col-sm col-2">{{ book.category }}</td>
          <td class="col-sm col-2">{{ book.language }}</td>
          <td class="col-sm col-1">{{ book.price }}</td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
import bookData from "../Data/booklist.json";
import bookCategorys from "../Data/bookCategory.json";
import { library } from "@fortawesome/fontawesome-svg-core";
import { fas } from "@fortawesome/free-solid-svg-icons";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

library.add(fas);

export default {
  components: {
    FontAwesomeIcon,
  },
  data() {
    return {
      books: bookData,
      bookCategorys: bookCategorys,
      selected: "",
      isItemSelected: false,
      isCategory: false,
      isBookName: false,
      isBookAuthor: false,
      selecteditems: [],
      noOfSelectBooks: 0,
    };
  },
  methods: {
    onChangeCategory(event) {
      if (event.target.value === "") {
        this.books = bookData;
      } else {
        this.books = bookData.filter((e) => e.category === event.target.value);
      }
    },
    onFilterOptionChange(event) {
      this.isCategory = false;
      this.isBookName = false;
      this.isBookAuthor = false;
      this.books = bookData;

      if (event.target.value === "2") {
        this.books.sort((a, b) => a.price - b.price);
      } else if (event.target.value === "3") {
        this.books.sort((a, b) => b.price - a.price);
      } else if (event.target.value === "4") {
        this.isBookName = true;
      } else if (event.target.value === "5") {
        this.isBookAuthor = true;
      } else if (event.target.value === "6") {
        this.isCategory = true;
      }
    },
    SearchBookByName(event) {
      const key = event.target.value.toLowerCase();
      const filterBooks = bookData;
      this.books = filterBooks.filter((e) =>
        e.bookname.toLowerCase().includes(key)
      );
    },
    SearchBookByAuthor(event) {
      const key = event.target.value.toLowerCase();
      const filterBooks = bookData;
      this.books = filterBooks.filter((e) =>
        e.author.toLowerCase().includes(key)
      );
    },
    onSelectBook(items) {
      if (this.selecteditems.length === 0) {
        this.selecteditems.push(items);
      } else if (!this.isBookSelected(items)) {
        this.selecteditems.push(items);
      } else {
        this.selecteditems = this.selecteditems.filter(
          (e) => e.id !== items.id
        );
      }

      this.noOfSelectBooks = this.selecteditems.length;
    },
    isBookSelected(book) {
      return this.selecteditems.some(
        (selectedBook) => selectedBook.id === book.id
      );
    },
    onPurchase() {
      this.$router.push({
        name: "BooksPayment",
        query: { yourItems: JSON.stringify(this.selecteditems) },
      });
    },
  },
  mounted() {
    this.selected = "";
  },
};
</script>

<style scoped>
.bodyDiv {
  width: 100%;
}
.filters {
  float: right;
  margin-right: 2.5%;
  height: 110px;
  text-align: end;
}

td,
th {
  padding: 15px 0px;
}

tr {
  border: 1px solid;
  min-height: 70px;
}
.bookNameRow {
  width: 300px;
}
.bookAuthorRow {
  width: 200px;
}
td:first-child {
  text-align: center;
}

tr:nth-child(odd) {
  background-color: rgb(190, 233, 233);
}

tr:first-child {
  background-color: rgb(12, 136, 136);
}

table {
  width: 95%;
  margin-left: 2.5%;
}

label {
  padding-right: 5px;
}
.filters :is(input, select) {
  width: 200px;
}

.mainFilter {
  margin-bottom: 5px;
}

.btn-success {
  background-color: #46e72dec;
  text-transform: uppercase;
}

.filters .btn-success {
  margin-bottom: 5px;
}
</style>
