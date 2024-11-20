<template>
  <div class="flex">
    <SideBar />

    <main class="flex-1 p-6">
      <div class="flex flex-col">
        <h1 class="text-2xl font-bold mb-4">Tra cứu Sách</h1>

        <div class="mb-6">
          <input
            v-model="searchQuery"
            @input="onSearch"
            type="text"
            placeholder="Nhập tên sách mà bạn muốn tìm..."
            class="border border-gray-300 rounded p-2 w-full"
          />
        </div>

        <DataTable
          :rows="filteredBooks"
          :columns="columns"
          :sortable="true"
          :filterable="true"
          :pagination="true"
          :rowsPerPage="5"
          :onView="handleView"
        >
          <template #status="slotProps">
            <span :class="slotProps.data.statusStyle">{{
              slotProps.data.status
            }}</span>
          </template>
        </DataTable>
      </div>
    </main>
  </div>
</template>

<script>
import DataTable from "@/components/commons/DataTable.vue";
import SideBar from "@/components/commons/SideBar.vue";
import bookService from "@/services/book.service";
import { ToVietnamCurrencyFormat } from "@/utils/ConvertCurrency";

export default {
  name: "SearchView",
  components: {
    DataTable,
    SideBar,
  },
  data() {
    return {
      searchQuery: "",
      books: [],
      columns: [
        { field: "id", header: "ID", sortable: true },
        { field: "title", header: "Tên Sách", sortable: true, filter: true },
        { field: "author", header: "Tác Giả", sortable: true, filter: true },
        { field: "price", header: "Giá mượn", sortable: true, filter: true },
        { field: "status", header: "Trạng Thái", sortable: true },
      ],
    };
  },
  computed: {
    filteredBooks() {
      const query = this.searchQuery.toLowerCase();
      return this.books.filter((book) => {
        return (
          book.title?.toLowerCase().includes(query) ||
          book.author?.toLowerCase().includes(query)
        );
      });
    },
  },
  methods: {
    async fetchBooks() {
      try {
        const response = await bookService.getAll();

        const bookArray = response.map((item) => {
          const isAvailable = item.quantity > 0;

          return {
            id: item?._id,
            title: item?.title,
            author: item?.author,
            price: ToVietnamCurrencyFormat(item?.price),
            status: isAvailable ? "Còn sách" : "Hết sách",
            statusStyle: isAvailable
              ? "text-green-500 font-bold"
              : "text-red-500 font-bold",
          };
        });
        this.books = bookArray;
      } catch (error) {
        console.error("Error fetching books:", error);
        alert("Không thể tải danh sách sách. Vui lòng thử lại sau.");
      }
    },
    onSearch() {
      console.log("Search query:", this.searchQuery);
    },
    handleView(book) {
      console.log("View Book:", book);
      alert(`Xem chi tiết: ${book.name}`);
    },
  },
  async created() {
    await this.fetchBooks();
  },
};
</script>

<style scoped></style>
