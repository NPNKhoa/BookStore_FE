<template>
  <div class="flex">
    <SideBar />

    <main class="flex-1 p-6">
      <div class="flex flex-col">
        <h1 class="text-2xl font-bold mb-4">Tìm Kiếm Sách</h1>

        <div class="mb-6">
          <input
            v-model="searchQuery"
            @input="onSearch"
            type="text"
            placeholder="Search"
            class="border border-gray-300 rounded p-2 w-full"
          />
        </div>

        <!-- Pass onView and onDelete to DataTable -->
        <DataTable
          :rows="filteredBooks"
          :columns="columns"
          :sortable="true"
          :filterable="true"
          :pagination="true"
          :rowsPerPage="5"
          v-model:selection="selectedBooks"
          :onView="handleView"
          :onDelete="handleDelete"
        />
      </div>

      <div class="mt-4">
        <h2 class="text-xl font-semibold">Sách đã chọn:</h2>
        <ul>
          <li v-for="book in selectedBooks" :key="book.id">
            {{ book.name }} - {{ book.author }}
          </li>
        </ul>
      </div>
    </main>
  </div>
</template>

<script>
import DataTable from "@/components/commons/DataTable.vue";
import SideBar from "@/components/commons/SideBar.vue";

export default {
  name: "SearchView",
  components: {
    DataTable,
    SideBar,
  },
  data() {
    return {
      searchQuery: "",
      selectedBooks: [],
      books: [
        {
          id: 1,
          name: "Book 1",
          author: "Author 1",
          price: 100000,
          quantity: 5,
          borrowDate: "2024-11-01",
        },
        {
          id: 2,
          name: "Book 2",
          author: "Author 2",
          price: 150000,
          quantity: 3,
          borrowDate: "2024-11-05",
        },
        {
          id: 3,
          name: "Book 3",
          author: "Author 3",
          price: 200000,
          quantity: 2,
          borrowDate: "2024-11-10",
        },
      ],
      columns: [
        { field: "id", header: "ID", sortable: true },
        { field: "name", header: "Tên Sách", sortable: true, filter: true },
        { field: "author", header: "Tác Giả", sortable: true, filter: true },
        { field: "price", header: "Đơn Giá", sortable: true },
        { field: "quantity", header: "Số Lượng", filter: true },
        { field: "borrowDate", header: "Ngày mượn", sortable: true },
      ],
    };
  },
  computed: {
    filteredBooks() {
      const query = this.searchQuery.toLowerCase();
      return this.books.filter((book) => {
        return (
          book.name.toLowerCase().includes(query) ||
          book.author.toLowerCase().includes(query)
        );
      });
    },
  },
  methods: {
    onSearch() {
      console.log("Search query:", this.searchQuery);
    },
    updateSelection(selection) {
      console.log("Selected books in SearchView:", selection);
      this.selectedBooks = selection;
    },
    handleView(book) {
      console.log("View Book:", book);
      alert(`Xem chi tiết: ${book.name}`);
    },
    handleDelete(book) {
      console.log("Delete Book:", book);
      this.books = this.books.filter((b) => b.id !== book.id);
      alert(`Xóa sách: ${book.name}`);
    },
  },
};
</script>

<style>
/* Add custom styles if necessary */
</style>
