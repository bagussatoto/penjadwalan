<template>
  <div>
    <!-- modal hapus jadwal start-->
    <div
      class="modal-back fixed top-0 left-0 right-0 bottom-0 bg-slate-700/50 min-h-screen flex"
      v-if="state_event"
    >
      <!-- modal content start -->
      <form
        class="p-8 bg-white w-96 m-auto h-72 rounded-lg flex justify-center items-center flex-col"
        data-cy="form-delete"
        name="delete"
      >
        <div
          class="logo px-5 py-4 w-16 rounded-full h-16 bg-red-400 text-3xl text-white flex justify-center items-center"
        >
          <font-awesome-icon icon="fa-solid fa-trash-can" class="m-auto" />
        </div>
        <h2 class="text-center mt-5 mb-5 text-2xl font-semibold">
          Hapus Mata Kuliah
        </h2>
        <p class="text-center text-slate-400">
          Apakah anda yakin ingin menghapus Statistika
        </p>

        <div class="text-white font-semibold flex justify-between w-full">
          <button
            class="px-6 py-2 bg-white border-2 border-red-400 text-red-400 rounded-full mt-5 shadow-lg shadow-red-300"
            data-cy="close-modal"
            @click="hide_event"
          >
            <font-awesome-icon icon="fa-solid fa-circle-xmark" />
            <span class="ml-2">Batal</span>
          </button>
          <button
            class="px-6 py-2 border-pink-400 border-2 bg-pink-400 rounded-full mt-5 shadow-lg shadow-pink-300"
            data-cy="btn-submit"
            @click="deleteItemSchedule(id_schedule)"
          >
            <font-awesome-icon icon="fa-solid fa-floppy-disk" />
            <span class="ml-2">Hapus</span>
          </button>
        </div>
      </form>
      <!-- modal content end -->
    </div>
    <!-- modal edit jadwal end-->
  </div>
</template>

<script>
export default {
  data() {
    return {
      idSchedule: 0,
    };
  },
  mounted() {
    // this.deleteItemSchedule(63);
  },
  props: ["state_event", "hide_event", "id_schedule"],
  methods: {
    async deleteItemSchedule(id) {
      await this.$axios.$delete(
        "schedule?email=" + localStorage.getItem("USER_EMAIL") + "&id=" + id
      );
      console.log(id);
      console.log(
        "schedule?email=" + localStorage.getItem("USER_EMAIL") + "&id=" + id
      );
    },
  },
};
</script>
