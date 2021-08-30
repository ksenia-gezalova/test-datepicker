<template>
  <div class="datepicker">
    <datepicker-header @goLast="goLast" @goNext="goNext" 
      @setCurrentYear="setCurrentYear" :currentDate="currentDate" />
    <datepicker-days :daysCount="daysCount" :nextMonthLabel="nextMonthName" 
      :startDayOfWeek="startDayOfWeek" />
  </div>
</template>

<script>
import DatepickerDays from '@/components/DatepickerDays.vue'
import DatepickerHeader from '@/components/DatepickerHeader.vue'
const START_YEAR = 1000;

export default {
  components: { DatepickerHeader, DatepickerDays },
  name: 'datepicker',
  data() {
    return {
      currentYear: '1994',
      currentMonth: 6,
      months: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 
      'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
      monthDayCount: [31, () => this.currentYear % 4 ? 28 : 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31],
    }
  },
  computed: {
    currentDate() {
      return {
        month: this.months[this.currentMonth],
        year: this.currentYear
      }
    },
    daysCount() {
      const days = this.monthDayCount[this.currentMonth];
      if (typeof(days) === 'function') return days();
      else return days;
    },
    nextMonthName() {
      return this.months[(this.currentMonth + 1) % 12];
    },
    startDayOfWeek() {
      let dayOfWeek = 2;
      dayOfWeek += (this.currentYear - START_YEAR) + Math.floor((this.currentYear - 1 - START_YEAR)/4);
      dayOfWeek += this.monthDayCount.slice(0, this.currentMonth)
        .map(month => typeof(month) === 'function' ? month() : month)
        .reduce((result, value) => result + value, 0);

      return dayOfWeek % 7;
    },
  },
  methods: {
    goLast() {
      if (this.currentMonth === 0) this.currentYear--;
      return this.currentMonth = (this.currentMonth + 11) % 12
    },
    goNext() {
      if (this.currentMonth === 11) this.currentYear++;
      return this.currentMonth = (this.currentMonth + 1) % 12
    },
    setCurrentYear(year) {
      if (!year) return;
      year = year.trim();
      if ((!(+year)) || year < 1000) return;
      this.currentYear = year;
    }
  }
}
</script>

<style lang="scss" scoped>
.datepicker {
  width: 310px;
  min-height: 260px;
  background-color: #fff;
  box-shadow: 0 2px 6px rgba(0,0,0,0.25);
}
</style>