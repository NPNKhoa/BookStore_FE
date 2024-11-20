<template>
  <div class="flex">
    <SideBar />

    <main class="flex-1 p-6">
      <div class="flex flex-col">
        <h1 class="text-2xl font-bold mb-4">Quản lý Sách</h1>

        <div class="flex justify-end gap-4 items-center w-1/4 ms-auto mb-4">
          <button
            class="bg-green-500 px-3 py-2 rounded-md flex items-center gap-1 text-white"
            @click="openAddBookModal"
          >
            <i class="pi pi-plus-circle"></i> Thêm mới sách
          </button>
          <button
            class="bg-blue-500 px-3 py-2 rounded-md flex items-center gap-1 text-white"
            @click="openEditBookModal"
          >
            <i class="pi pi-pen-to-square"></i> Chỉnh sửa
          </button>
        </div>

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

        <!-- Modal chi tiết sách -->
        <CustomModal
          :visible="isDetailModalVisible"
          header="Chi tiết sách"
          :onCancel="closeDetailModal"
          @update:visible="isDetailModalVisible = $event"
        >
          <div class="flex flex-col gap-2 text-xl">
            <p><strong>Tiêu đề:</strong> {{ detailedBook.title }}</p>
            <p><strong>Giá:</strong> {{ detailedBook.price }}</p>
            <p><strong>Số lượng:</strong> {{ detailedBook.quantity }}</p>
            <p><strong>Năm xuất bản:</strong> {{ detailedBook.publishYear }}</p>
            <p><strong>Nhà xuất bản:</strong> {{ detailedBook.publisher }}</p>
            <p><strong>Tác giả:</strong> {{ detailedBook.author }}</p>
            <p>
              <strong>Trạng thái: </strong>
              <span
                :class="
                  detailedBook.quantity > 0 ? 'text-green-500' : 'text-red-500'
                "
              >
                {{ detailedBook.quantity > 0 ? "Còn sách" : "Hết sách" }}
              </span>
            </p>
          </div>
        </CustomModal>
      </div>
    </main>
  </div>
</template>

<script>
import DataTable from "@/components/commons/DataTable.vue";
import SideBar from "@/components/commons/SideBar.vue";
import CustomModal from "@/components/commons/CustomModal.vue";
import { ToVietnamCurrencyFormat } from "@/utils/ConvertCurrency";
import bookService from "@/services/book.service";

export default {
  name: "BooksView",
  components: {
    DataTable,
    SideBar,
    CustomModal,
  },
  data() {
    return {
      searchQuery: "",
      selectedBooks: [],
      books: [],
      columns: [
        { field: "id", header: "ID", sortable: true },
        { field: "title", header: "Tên Sách", sortable: true, filter: true },
        { field: "author", header: "Tác Giả", sortable: true, filter: true },
        {
          field: "publisher",
          header: "Nhà Xuất Bản",
          sortable: true,
          filter: true,
        },
        { field: "price", header: "Đơn Giá", sortable: true },
        { field: "quantity", header: "Số Lượng", filter: true },
      ],
      isModalVisible: false,
      modalHeader: "",
      isDetailModalVisible: false,
      detailedBook: {},
      currentBook: this.createEmptyBook(),
      isEditing: false,
    };
  },
  computed: {
    filteredBooks() {
      const query = this.searchQuery.toLowerCase();
      return this.books.filter((book) => {
        return (
          book?.title?.toLowerCase()?.includes(query) ||
          book?.author?.toLowerCase()?.includes(query)
        );
      });
    },
  },
  methods: {
    async fetchBooks() {
      try {
        const response = await bookService.getAll();

        const bookArray = response.map((item) => {
          return {
            id: item?._id,
            title: item?.title,
            author: item?.author,
            publisher: item?.publisherId?.publisherName,
            price: ToVietnamCurrencyFormat(item?.price),
            quantity: item?.quantity,
          };
        });
        this.books = bookArray;
      } catch (error) {
        console.error("Error fetching books:", error);
        alert("Không thể tải danh sách sách. Vui lòng thử lại sau.");
      }
    },
    handleView(book) {
      this.fetchBookDetails(book.id);
    },
    async fetchBookDetails(id) {
      try {
        const book = await bookService.get(id);
        this.detailedBook = {
          title: book.title,
          price: ToVietnamCurrencyFormat(book.price),
          quantity: book.quantity,
          publishYear: book.publishYear,
          publisher: book.publisherId.publisherName,
          author: book.author,
        };
        this.isDetailModalVisible = true;
      } catch (error) {
        console.error("Error fetching book details:", error);
        alert("Không thể xem chi tiết sách. Vui lòng thử lại sau.");
      }
    },
    closeDetailModal() {
      this.isDetailModalVisible = false;
    },
    createEmptyBook() {
      return {
        id: null,
        title: "",
        author: "",
        price: null,
        quantity: null,
        publishYear: null,
        publisher: "",
      };
    },
    openAddBookModal() {
      console.log("ok");
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
  async created() {
    await this.fetchBooks();
  },
};
</script>
