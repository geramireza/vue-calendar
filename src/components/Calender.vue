<template>
  <h2 class="">Vue Calender</h2>

  <div class="d-flex justify-content-between mt-4">
    <h3>{{ currentMonthName }}</h3>
    <h3>{{ currentYear }}</h3>
  </div>
  <div class="table-responsive">
    <table
      class="table text-center border-default"
      style="border-collapse: collapse !important"
    >
      <thead class="table-primary">
        <tr class="d-flex">
          <th
            class="flex-fill py-3 border border-info"
            style="width: 14.28%"
            v-for="weekDay in weekDays"
            :key="weekDay"
          >
            {{ weekDay }}
          </th>
        </tr>
      </thead>
      <tbody>
        <tr class="d-flex flex-wrap">
          <td
            class="py-3 border"
            style="width: 14.28%"
            v-for="num in startDayInWeek"
            :key="num"
          ></td>
          <td
            style="width: 14.28%"
            v-for="day in daysInCurrentMonth"
            :key="day"
            class="py-3 border"
            :class="currentDateClass(day)"
          >
            {{ day }}
          </td>
        </tr>
      </tbody>
    </table>
    <div class="d-flex justify-content-between mb-5">
      <button type="button" class="btn btn-secondary" @click="prev">
        Prev
      </button>
      <button
        v-if="!isCurrentMonthAndYear"
        type="button"
        class="btn btn-secondary"
        @click="current"
      >
        Current
      </button>
      <button type="button" class="btn btn-secondary" @click="next">
        Next
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      weekDays: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"],
      currentMonth: new Date().getMonth(),
      currentYear: new Date().getFullYear(),
      currentDate: new Date().getDate(),
    };
  },
  methods: {
    prev() {
      if (this.currentMonth == 0) {
        this.currentMonth = 11;
        this.currentYear--;
      } else {
        this.currentMonth--;
      }
    },
    next() {
      if (this.currentMonth == 11) {
        this.currentMonth = 0;
        this.currentYear++;
      } else {
        this.currentMonth++;
      }
    },
    current(){
        this.currentMonth = new Date().getMonth()
        this.currentYear = new Date().getFullYear()

    },
    currentDateClass(day) {
      const calendarFullDate = new Date(this.currentYear, this.currentMonth, day).toDateString()
      const currentFullDate =  new Date().toDateString()
      return calendarFullDate === currentFullDate
        ? "table-active border-info"
        : "";
    },
  },
  computed: {
    daysInCurrentMonth() {
      return new Date(this.currentYear, this.currentMonth + 1, 0).getDate();
    },
    startDayInWeek() {
      return new Date(this.currentYear, this.currentMonth, 1).getDay();
    },
    currentMonthName() {
      return new Date(
        this.currentYear,
        this.currentMonth
      ).toLocaleString("en-US", { month: "long" });
    },
    isCurrentMonthAndYear(){
        return this.isCurrentMonth && this.isCurrentYear
    },
    isCurrentMonth(){
        return this.currentMonth === new Date().getMonth()
    },
    isCurrentYear(){
        return this.currentYear === new Date().getFullYear()
    }
  },
  mounted() {},
};
</script>

<style>
</style>