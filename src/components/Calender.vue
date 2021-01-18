<template>
  <div>
    <h2 class="mb-3">Vue Calendar</h2>
    <div class="d-flex justify-content-between">
      <h3>{{ currentMontName }}</h3>
      <h3>{{ currentYear }}</h3>
    </div>
    <div class="table-responsive">
      <table class="table text-center">
        <thead class="table-primary">
          <tr class="d-flex">
            <th
              style="width: 14.28%"
              class="flex-fill px-1 py-3 border-top-0 border-start-0 border-end-0 border-info"
              v-for="dayOfWeek in daysOfWeek"
              :key="dayOfWeek"
            >
              {{ dayOfWeek }}
            </th>
          </tr>
        </thead>
        <tbody>
          <tr class="d-flex flex-wrap">
            <td
              class="border-bottom-0 border-end-0 border px-1 py-3 text-muted"
              style="width: 14.28%"
              v-for="day in startOfMonth"
              :key="day"
            >
              0{{ day }}
            </td>

            <td
              class="border-bottom-0 border-end-0 border px-1 py-3 text-dark"
              style="width: 14.28%"
              v-for="day in totalDaysInMonth"
              :key="day"
              :class="currentDateActiveClass(day)"
            >
              {{ fullDay(day) }}

            </td>

            <td
              class="border-bottom-0 border-end-0 border px-1 py-3 text-muted"
              style="width: 14.28%"
              v-for="day in endOfMonth"
              :key="day"
            >
              0{{ day }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="d-flex justify-content-between mt-4">
      <button type="button" class="btn btn-secondary" @click="prev">
        Prev
      </button>
      <button type="button" class="btn btn-secondary rounded-pill" v-if=" !(isCurrentMonth && isCurrentYear) "  @click="current">
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
      daysOfWeek: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"],
      currentMonth: new Date().getMonth(),
      currentYear: new Date().getFullYear(),
    };
  },
  methods: {
    next() {
      if (this.currentMonth == 11) {
        this.currentMonth = 0;
        this.currentYear++;
      } else {
        this.currentMonth++;
      }
    },
    prev() {
      if (this.currentMonth == 0) {
        this.currentMonth = 11;
        this.currentYear--;
      } else {
        this.currentMonth--;
      }
    },
    current(){
      this.currentMonth = new Date().getMonth()
      this.currentYear = new Date().getFullYear()
    },
    fullDay(day) {
      return day.toString().length >= 2 ? day : "0" + day;
    },
  currentDateActiveClass(day){
        const calendarFullDate = new Date(this.currentYear,this.currentMonth,day).toDateString()
        const currentFullDate = new Date().toDateString();
         return calendarFullDate == currentFullDate ? 'table-active' : ''
    }
  },
  computed: {
    currentMontName() {
      return new Date(
        this.currentYear,
        this.currentMonth
      ).toLocaleString("en-US", { month: "long" });
    },
    totalDaysInMonth() {
      return new Date(this.currentYear, this.currentMonth + 1, 0).getDate();
    },
    startOfMonth() {
      return new Date(this.currentYear, this.currentMonth, 1).getDay();
    },
    endOfMonth() {
      return (
        this.daysOfWeek.length -
        (new Date(this.currentYear, this.currentMonth + 1, 0).getDay() + 1)
      );
    },
    isCurrentMonth(){
      return this.currentMonth === new Date().getMonth()
    },
    isCurrentYear(){
      return this.currentYear === new Date().getFullYear()
    }
    
  },
  mounted() {
  },
};
</script>

<style>
tbody td:nth-child(7n),
td:last-child {
  border-right: 1px solid #dee2e6 !important;
}
tbody td:nth-last-child(-n + 7) {
  border-bottom: 1px solid #dee2e6 !important;
}
</style>
