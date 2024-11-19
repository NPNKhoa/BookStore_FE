<template>
  <div class="flex">
    <SideBar />

    <main class="flex-1 p-6">
      <div class="flex flex-col">
        <h1 class="text-2xl font-bold mb-4">Quản lý Sách</h1>

        <div class="flex justify-end gap-4 items-center w-1/4 ms-auto mb-4">
          <button
            class="bg-green-500 px-3 py-2 rounded-md flex items-center gap-1"
            @click="openAddBookModal"
          >
            <i class="pi pi-plus-circle"></i> Thêm mới sách
          </button>
          <button
            class="bg-blue-500 px-3 py-2 rounded-md flex items-center gap-1"
            @click="openEditBookModal"
          >
            <i class="pi pi-pen-to-square"></i> Chỉnh sửa
          </button>
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

        <CustomModal
          :visible="isModalVisible"
          :header="modalHeader"
          :onOk="handleModalOk"
          :onCancel="handleModalCancel"
          @update:visible="isModalVisible = $event"
        >
          <!-- Nội dung modal -->
          <form>
            <div class="mb-4">
              <label class="block font-medium">Title</label>
              <input
                type="text"
                v-model="currentBook.name"
                class="w-full p-2 border border-gray-300 rounded"
              />
            </div>
            <div class="mb-4">
              <label class="block font-medium">Price</label>
              <input
                type="number"
                v-model="currentBook.price"
                class="w-full p-2 border border-gray-300 rounded"
              />
            </div>
            <div class="mb-4">
              <label class="block font-medium">Quantity</label>
              <input
                type="number"
                v-model="currentBook.quantity"
                class="w-full p-2 border border-gray-300 rounded"
              />
            </div>
            <div class="mb-4">
              <label class="block font-medium">Publish Year</label>
              <input
                type="number"
                v-model="currentBook.publishYear"
                class="w-full p-2 border border-gray-300 rounded"
              />
            </div>
            <div class="mb-4">
              <label class="block font-medium">Publisher</label>
              <input
                type="text"
                v-model="currentBook.publisher"
                class="w-full p-2 border border-gray-300 rounded"
              />
            </div>
            <div class="mb-4">
              <label class="block font-medium">Author Name</label>
              <input
                type="text"
                v-model="currentBook.author"
                class="w-full p-2 border border-gray-300 rounded"
              />
            </div>
          </form>
        </CustomModal>
      </div>
    </main>
  </div>
</template>

<script>
import DataTable from "@/components/commons/DataTable.vue";
import SideBar from "@/components/commons/SideBar.vue";
import CustomModal from "@/components/commons/CustomModal.vue";

export default {
  name: "SearchView",
  components: {
    DataTable,
    SideBar,
    CustomModal,
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
      isModalVisible: false,
      modalHeader: "",
      currentBook: this.createEmptyBook(),
      isEditing: false,
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
    createEmptyBook() {
      return {
        id: null,
        name: "",
        author: "",
        price: null,
        quantity: null,
        publishYear: null,
        publisher: "",
      };
    },
    openAddBookModal() {
      this.modalHeader = "Thêm mới sách";
      this.currentBook = this.createEmptyBook();
      this.isEditing = false;
      this.isModalVisible = true;
    },
    openEditBookModal() {
      if (this.selectedBooks.length !== 1) {
        alert("Vui lòng chọn một sách để chỉnh sửa.");
        return;
      }
      this.modalHeader = "Chỉnh sửa sách";
      this.currentBook = { ...this.selectedBooks[0] };
      this.isEditing = true;
      this.isModalVisible = true;
    },
    handleModalOk() {
      if (this.isEditing) {
        const index = this.books.findIndex(
          (book) => book.id === this.currentBook.id
        );
        this.books[index] = { ...this.currentBook };
      } else {
        this.currentBook.id = this.books.length + 1;
        this.books.push({ ...this.currentBook });
      }
      this.isModalVisible = false;
    },
    handleModalCancel() {
      this.isModalVisible = false;
    },
  },
};
</script>
