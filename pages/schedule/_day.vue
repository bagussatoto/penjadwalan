<template>
  <div>
    <header class="p-5 w-full bg-black text-white">
      <div class="container md:max-w-5xl flex justify-between m-auto">
        <h1 class="font-semibold text-3xl">GetJadwal</h1>
        <button
          class="btn px-4 py-2 bg-pink-400 rounded-lg font-semibold"
          data-cy="btn-logout"
          @click="logout"
        >
          Check Out | {{ email }}
        </button>
      </div>
    </header>
    <div class="min-h-screen h-auto relative w-full bg-slate-200">
      <div class="container md:max-w-5xl m-auto">
        <div
          class="flex justify-between pt-8 pb-8 mb-5 items-center"
          style="border-bottom: 2px solid rgba(0, 0, 0, 0.15)"
        >
          <div class="text-2xl">
            <nuxt-link to="/home">
              <font-awesome-icon
                icon="fa-solid fa-chevron-left"
                data-cy="btn-back"
              />
              <span class="day ml-2 font-semibold" data-cy="detail-title">{{
                $route.params.day === "monday"
                  ? "Senin"
                  : $route.params.day === "tuesday"
                  ? "Selasa"
                  : $route.params.day === "wednesday"
                  ? "Rabu"
                  : $route.params.day === "thursday"
                  ? "Kamis"
                  : "Jumat"
              }}</span>
            </nuxt-link>
          </div>
          <button
            class="rounded-full bg-pink-400 hover:bg-pink-500 active:bg-pink-600 text-white h-14 px-4 py-4 font-bold shadow-lg shadow-pink-300"
            data-cy="btn-create-schedule"
            @click="showAddModalBox"
          >
            <font-awesome-icon icon="fa-solid fa-plus" />
            <span class="ml-2">Tambah Mata Kuliah</span>
          </button>
        </div>

        <ImageEmptyItem
          :condition="scheduleLength"
          v-if="listSchedules.length == 0"
        />

        <!-- list item MK start-->
        <div class="container w-full mt-5" v-for="item in listSchedules">
          <CardDetailItem :nama_mk="item.title" :id_mk="item.id" />
        </div>
        <!-- list item MK end -->
      </div>
    </div>

    <DetailModalBoxAdd
      :state_event="isShowAddModalBox"
      :hide_event="hideAddModalBox"
    />

    <!-- toast start -->
    <p
      class="toast px-3 py-2 w-72 m-auto rounded-lg bg-green-400 inlineblock absolute top-16 left-0 right-0 shadow shadow-green-200 hidden"
    >
      <font-awesome-icon icon="fa-solid fa-circle-check" class="ml-2" />
      <span class="ml-2"> mata kuliah berhasil dihapus </span>
    </p>
    <!-- toast end -->
  </div>
</template>

<script>
import CardDetailItem from "~/components/CardDetailItem.vue";
import DetailModalBoxDelete from "~/components/DetailModalBoxDelete.vue";
import ImageEmptyItem from "~/components/ImageEmptyItem.vue";

const userEmail = process.server ? "" : localStorage.getItem("USER_EMAIL");
// ketika script diload di sisi client
let backToLogin;
if (process.client) {
  backToLogin = () => {
    window.location.replace("/");
  };
  // jika email tidak terdaftar maka kembali ke halaman index/login
  if (userEmail === "") {
    backToLogin();
  }
}

export default {
  data() {
    return {
      isShowEditModalBox: false,
      isShowAddModalBox: false,
      isShowDeleteModalBox: false,
      isShowToast: false,
      email: userEmail,
      scheduleLength: 0,
      listSchedules: [],
      day: this.$route.params.day,
    };
  },
  mounted() {
    this.checkCredential();
    this.getDetailSchedule();
  },

  methods: {
    async getDetailSchedule() {
      await this.$axios
        .$get(
          "/schedule?email=" +
            localStorage.getItem("USER_EMAIL") +
            "&day=" +
            this.day
        )
        .then((response) => {
          this.listSchedules = response.data;
          console.log(this.listSchedules);
        });
    },

    checkCredential() {
      if (!process.server) {
        const emailValid = localStorage.getItem("USER_EMAIL");
        if (!emailValid || emailValid === "") {
          window.location.assign("/");
        }
      }
    },

    // toggle state
    showAddModalBox() {
      this.isShowAddModalBox = true;
      console.log(this.day);
    },

    showToast() {
      this.isShowToast = true;
    },
    hideAddModalBox() {
      this.isShowAddModalBox = false;
    },
    hideToast() {
      this.isShowToast = false;
    },
    logout() {
      localStorage.clear();
      backToLogin();
    },
  },
  components: { DetailModalBoxDelete, CardDetailItem, ImageEmptyItem },
};
</script>
