<template>
  <div class="flex h-screen">
    <div class="flex-1 bg-green-100 flex items-center justify-center">
      <div class="text-center">
        <h1 class="text-3xl font-semibold mb-2">Phần mềm quản lý thư viện</h1>
        <p class="text-gray-600 text-xl">Book Management System</p>
      </div>
    </div>

    <div class="flex-1 bg-white flex items-center justify-center">
      <div class="w-96 px-8 py-12 bg-white rounded shadow-lg shadow-slate-400">
        <h2 class="text-2xl font-semibold mb-4 text-center">Đăng Nhập</h2>

        <form @submit.prevent="handleLogin">
          <div class="mb-4">
            <input
              v-model="email"
              type="email"
              id="email"
              class="mt-1 block w-full border border-gray-300 rounded py-2 px-3 shadow-sm focus:ring-blue-500 focus:border-blue-500"
              placeholder="Email"
              required
            />
          </div>

          <div class="mb-4">
            <input
              v-model="password"
              type="password"
              id="password"
              class="mt-1 block w-full border border-gray-300 rounded py-2 px-3 shadow-sm focus:ring-blue-500 focus:border-blue-500"
              placeholder="Mật khẩu"
              required
            />
          </div>

          <button
            type="submit"
            class="w-full bg-blue-600 text-white py-2 px-4 rounded hover:bg-blue-700"
          >
            Đăng Nhập
          </button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "LoginView",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    handleLogin() {
      console.log("Email:", this.email);
      console.log("Password:", this.password);
      alert("Đăng nhập thành công!");
    },
  },
};
</script>

<style scoped></style>
