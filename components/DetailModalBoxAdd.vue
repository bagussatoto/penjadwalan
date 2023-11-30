<template>
  <div>
    <!-- modal add jadwal start-->
    <div
      class="modal-back fixed top-0 left-0 right-0 bottom-0 bg-slate-700/50 min-h-screen flex"
      v-if="state_event"
    >
      <!-- modal content start -->
      <form
        class="p-8 bg-white w-96 m-auto h-72 rounded-lg"
        data-cy="form-add"
        name="add"
      >
        <h2 class="text-center mb-5 text-2xl font-semibold">
          Buat Jadwal Kuliah
        </h2>
        <label
          for="add-matkul"
          class="font-semibold border-t-2 w-full block pt-3"
          >Mata Kuliah</label
        >
        <input
          type="text"
          name="add-matkul"
          data-cy="form-matkul"
          v-model="newSchedule"
          id="add-matkul"
          class="outline block outline-1 px-3 py-2 rounded-lg outline-slate-300 mt-1 w-full mb-5 focus:outline-2 focus:outline-pink-400"
          placeholder="Masukan Mata Kuliah"
        />

        <div
          class="mt-6 text-white border-t-2 font-semibold flex justify-between"
        >
          <button
            class="px-6 py-2 bg-white border-2 border-red-400 text-red-400 rounded-full mt-5 shadow-lg shadow-red-300"
            data-cy="close-modal"
            @click="hide_event"
          >
            <font-awesome-icon icon="fa-solid fa-circle-xmark" />
            <span class="ml-2">Batalkan</span>
          </button>
          <button
            class="px-6 py-2 border-pink-400 border-2 bg-pink-400 rounded-full mt-5 shadow-lg shadow-pink-300"
            data-cy="btn-submit"
            @click="addScheduleItem"
            v-if="newSchedule"
          >
            <font-awesome-icon icon="fa-solid fa-floppy-disk" />
            <span class="ml-2">Simpan</span>
          </button>

          <button
            class="px-6 py-2 border-slate-400 border-2 bg-slate-400 rounded-full mt-5 shadow-lg shadow-slate-300 cursor-not-allowed"
            data-cy="btn-submit"
            disabled
            v-else
          >
            <font-awesome-icon icon="fa-solid fa-floppy-disk" />
            <span class="ml-2">Simpan</span>
          </button>
        </div>
      </form>
      <!-- modal content end -->
    </div>
    <!-- modal add jadwal end-->
  </div>
</template>

<script>
export default {
  data() {
    return {
      newSchedule: "",
    };
  },
  props: ["state_event", "hide_event", "submit_event"],
  methods: {
    async addScheduleItem() {
      await this.$axios
        .$post("schedule?email=" + localStorage.getItem("USER_EMAIL"), {
          title: this.newSchedule,
          day: this.$route.params.day,
        })
        .then((response) => {
          const result = response.data;
          console.log(result);
          console.log(this.day);
        });
    },
  },
};
</script>
