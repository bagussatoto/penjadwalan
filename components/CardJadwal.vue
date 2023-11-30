<template>
  <div class="w-full flex gap-2">
    <div class="w-full" v-for="(schedule, day) in listSchedules">
      <div class="head p-5 bg-white special-round">
        <nuxt-link :to="'/schedule/' + day">
          <p class="day font-semibold text-2xl" :data-cy="'card-title-' + day">
            {{
              day === "monday"
                ? "Senin"
                : day === "tuesday"
                ? "Selasa"
                : day === "wednesday"
                ? "Rabu"
                : day === "thursday"
                ? "Kamis"
                : "Jumat"
            }}
          </p>
          <p
            v-if="schedule === 0"
            class="desc text-slate-400 text-sm"
            :data-cy="'card-desc-' + day"
          >
            Belum ada mata kuliah
          </p>
          <p
            v-else
            class="desc text-pink-400 text-sm"
            :data-cy="'card-desc-' + day"
          >
            {{ schedule }} Mata Kuliah
          </p>
        </nuxt-link>
      </div>

      <!-- list item schedule monday start -->
      <div class="body p-2 bg-white mt-5 special-round" v-if="day === 'monday'">
        <div
          class="item p-3 bg-slate-100 mb-1"
          v-for="item in listItemScheduleMonday"
        >
          {{ item.title }}
        </div>
      </div>
      <!-- list item schedule monday end -->

      <!-- list item schedule tuesday start -->
      <div
        class="body p-2 bg-white mt-5 special-round"
        v-if="day === 'tuesday'"
      >
        <div
          class="item p-3 bg-slate-100 mb-1"
          v-for="item in listItemScheduleTuesday"
        >
          {{ item.title }}
        </div>
      </div>
      <!-- list item schedule tuesday end -->

      <!-- list item schedule wednesday start -->
      <div
        class="body p-2 bg-white mt-5 special-round"
        v-if="day === 'wednesday'"
      >
        <div
          class="item p-3 bg-slate-100 mb-1"
          v-for="item in listItemScheduleWednesday"
        >
          {{ item.title }}
        </div>
      </div>
      <!-- list item schedule wednesday end -->

      <!-- list item schedule thursday start -->
      <div
        class="body p-2 bg-white mt-5 special-round"
        v-if="day === 'thursday'"
      >
        <div
          class="item p-3 bg-slate-100 mb-1"
          v-for="item in listItemScheduleThursday"
        >
          {{ item.title }}
        </div>
      </div>
      <!-- list item schedule thursday end -->

      <!-- list item schedule friday start -->
      <div class="body p-2 bg-white mt-5 special-round" v-if="day === 'friday'">
        <div
          class="item p-3 bg-slate-100 mb-1"
          v-for="item in listItemScheduleFriday"
        >
          {{ item.title }}
        </div>
      </div>
      <!-- list item schedule friday end -->
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      listSchedules: [],
      listItemScheduleMonday: [],
      listItemScheduleTuesday: [],
      listItemScheduleWednesday: [],
      listItemScheduleThursday: [],
      listItemScheduleFriday: [],
    };
  },
  mounted() {
    this.getAllSchedule();
  },
  methods: {
    async getAllSchedule() {
      await this.$axios
        .$get("/schedule?email=" + localStorage.getItem("USER_EMAIL"))
        .then((response) => {
          const result = (this.listSchedules = response.data);
          console.log(result);
        });

      // fetch item schedule monday
      await this.$axios
        .$get(
          "/schedule?email=" +
            localStorage.getItem("USER_EMAIL") +
            "&day=monday"
        )
        .then((response) => {
          const result = response.data;
          this.listItemScheduleMonday = result;
        });

      // fetch item schedule monday
      await this.$axios
        .$get(
          "/schedule?email=" +
            localStorage.getItem("USER_EMAIL") +
            "&day=monday"
        )
        .then((response) => {
          const result = response.data;
          this.listItemScheduleMonday = result;
        });

      // fetch item schedule tuesday
      await this.$axios
        .$get(
          "/schedule?email=" +
            localStorage.getItem("USER_EMAIL") +
            "&day=tuesday"
        )
        .then((response) => {
          const result = response.data;
          this.listItemScheduleTuesday = result;
        });

      // fetch item schedule wednesday
      await this.$axios
        .$get(
          "/schedule?email=" +
            localStorage.getItem("USER_EMAIL") +
            "&day=wednesday"
        )
        .then((response) => {
          const result = response.data;
          this.listItemScheduleWednesday = result;
        });

      // fetch item schedule thursday
      await this.$axios
        .$get(
          "/schedule?email=" +
            localStorage.getItem("USER_EMAIL") +
            "&day=thursday"
        )
        .then((response) => {
          const result = response.data;
          this.listItemScheduleThursday = result;
        });

      // fetch item schedule friday
      await this.$axios
        .$get(
          "/schedule?email=" +
            localStorage.getItem("USER_EMAIL") +
            "&day=friday"
        )
        .then((response) => {
          const result = response.data;
          this.listItemScheduleFriday = result;
        });
    },
  },
};
</script>

<style>
.special-round {
  @apply rounded-lg shadow-lg shadow-pink-200;
}
</style>
