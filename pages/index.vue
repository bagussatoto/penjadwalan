<template>
  <div>
    <header class="p-5 w-full text-center bg-black fixed text-white">
      <h1 class="font-semibold text-3xl">GetJadwal</h1>
    </header>
    <div class="h-screen w-full bg-slate-200 flex justify-center">
      <!-- card start -->
      <div class="px-10 py-5 bg-white w-96 h-80 mt-48 rounded-md shadow-lg">
        <h1
          class="text-center font-semibold text-2xl mb-10 mt-5"
          data-cy="text-login"
        >
          Check In
        </h1>
        <label for="email" class="block">Email</label>
        <input
          type="email"
          name="email"
          id="email"
          class="bg-slate-100 rounded-md block border-spacing-1 mb-2 p-3 w-full border-2 border-slate-300 outline-2 focus:outline-pink-400"
          placeholder="masukan alamat email anda"
          data-cy="input-email"
          required
          v-model="email"
        />
        <div class="if" v-if="error">
          <p class="text-red-500">
            <font-awesome-icon icon="fa-solid fa-circle-info" />
            <span class="ml-1" data-cy="error-email"
              >format email tidak sesuai</span
            >
          </p>
        </div>

        <button
          v-if="error === true || email === ''"
          class="rounded-full mt-3 shadow-lg shadow-slate-300 bg-slate-400 text-white px-2 py-4 w-full font-bold cursor-not-allowed"
          data-cy="btn-login"
          disabled
        >
          Mulai Sesi
        </button>

        <button
          v-else
          class="rounded-full mt-3 shadow-lg shadow-pink-300 bg-pink-400 active:bg-pink-600 text-white px-2 py-4 w-full font-bold cursor-pointer"
          data-cy="btn-login"
          @click="checkinEmail"
        >
          Mulai Sesi
        </button>
      </div>
      <!-- card end -->
    </div>
  </div>
</template>

<script>
export default {
  name: "IndexPage",
  data() {
    return {
      error: false,
      email: "",
      savedEmail: "",
      savedId: "",
    };
  },
  methods: {
    async checkinEmail() {
      try {
        await this.$axios
          .$post("/checkin", {
            email: this.email,
          })
          .then((response) => {
            const result = response.data;
            console.log(result);
            this.savedEmail = result.email;
            localStorage.setItem("USER_EMAIL", this.savedEmail);
            console.log(localStorage.getItem("USER_EMAIL"));
            window.location.replace("/home");
          });
      } catch (error) {
        this.error = true;
      }
    },
  },
};
</script>
