<template>
  <div class="flex">
    <Sidebar />

    <main class="flex-1 p-6 w-full">
      <h1 class="text-2xl font-bold mb-6">Lịch Sử Mượn Sách</h1>

      <button
        @click="openModal"
        class="bg-green-500 text-white py-3 px-6 rounded-md ms-auto mb-4 flex justify-between items-center gap-4"
      >
        <i class="pi pi-plus"></i> Thuê sách
      </button>

      <DataTable
        :rows="books"
        :columns="columns"
        :sortable="true"
        :filterable="true"
        :pagination="true"
        :rowsPerPage="5"
      />

      <div
        v-if="isModalOpen"
        class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50"
      >
        <div class="bg-white rounded-lg p-6 w-96">
          <h2 class="text-xl font-bold mb-4">Thuê Sách</h2>
          <form @submit.prevent="handleSubmit">
            <div class="mb-4">
              <label
                for="reader"
                class="block text-sm font-medium text-gray-700"
              >
                Độc giả
              </label>
              <select
                v-model="form.reader"
                id="reader"
                class="mt-1 block w-full border border-gray-300 rounded py-2 px-3 shadow-sm focus:ring-green-500 focus:border-green-500"
                required
              >
                <option value="" disabled>Chọn độc giả</option>
                <option
                  v-for="reader in readers"
                  :key="reader.id"
                  :value="reader.id"
                >
                  {{ reader.name }}
                </option>
              </select>
            </div>

            <div class="mb-4">
              <label for="book" class="block text-sm font-medium text-gray-700">
                Sách
              </label>
              <select
                v-model="form.book"
                id="book"
                class="mt-1 block w-full border border-gray-300 rounded py-2 px-3 shadow-sm focus:ring-green-500 focus:border-green-500"
                required
              >
                <option value="" disabled>Chọn sách</option>
                <option v-for="book in books" :key="book.id" :value="book.id">
                  {{ book.name }}
                </option>
              </select>
            </div>

            <!-- Ngày mượn -->
            <div class="mb-4">
              <label
                for="borrowDate"
                class="block text-sm font-medium text-gray-700"
              >
                Ngày mượn
              </label>
              <input
                v-model="form.borrowDate"
                type="date"
                id="borrowDate"
                class="mt-1 block w-full border border-gray-300 rounded py-2 px-3 shadow-sm focus:ring-green-500 focus:border-green-500"
                required
              />
            </div>

            <!-- Nút Submit và Hủy -->
            <div class="flex justify-end gap-2">
              <button
                type="button"
                @click="closeModal"
                class="bg-gray-400 text-white py-2 px-4 rounded hover:bg-gray-500"
              >
                Hủy
              </button>
              <button
                type="submit"
                class="bg-green-500 text-white py-2 px-4 rounded hover:bg-green-600"
              >
                Xác nhận
              </button>
            </div>
          </form>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import Sidebar from "@/components/commons/SideBar.vue";
import DataTable from "@/components/commons/DataTable.vue";

export default {
  name: "HomeView",
  components: {
    Sidebar,
    DataTable,
  },
  data() {
    return {
      isModalOpen: false,
      form: {
        reader: "",
        book: "",
        borrowDate: "",
      },
      readers: [
        { id: 1, name: "Độc giả 1" },
        { id: 2, name: "Độc giả 2" },
        { id: 3, name: "Độc giả 3" },
      ],
      books: [
        {
          id: 1,
          name: "Book 1",
          author: "Author 1",
          price: 100000,
          quantity: 5,
        },
        {
          id: 2,
          name: "Book 2",
          author: "Author 2",
          price: 150000,
          quantity: 3,
        },
        {
          id: 3,
          name: "Book 3",
          author: "Author 3",
          price: 200000,
          quantity: 7,
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
  methods: {
    openModal() {
      this.isModalOpen = true;
    },
    closeModal() {
      this.isModalOpen = false;
      this.resetForm();
    },
    resetForm() {
      this.form = {
        reader: "",
        book: "",
        borrowDate: "",
      };
    },
    handleSubmit() {
      console.log("Thuê sách:", this.form);
      alert("Thuê sách thành công!");
      this.closeModal();
    },
  },
};
</script>

<style scoped></style>
