<template>
  <div class="days">
    <div class="days__container">
      <span v-for="index in startDayOfWeek" :key="index"></span>
      <datepicker-day v-for="index in daysCount" :day="index" :key="index" />
      <datepicker-day v-for="index in nextMonthDays" :day="index" isNextMonth :nextMonthLabel="nextMonthLabel" :key="index" />
    </div>
  </div>
</template>

<script>
import DatepickerDay from '@/components/DatepickerDay.vue'
const DAYS_COUNT = 42;

export default {
  name: 'DatepickerDays',
  components: { DatepickerDay },
  props: {
    daysCount: {
      type: [Number, String],
    },
    nextMonthLabel: {
      type: String,
    },
    startDayOfWeek: {
      type: Number,
    }
  },
  computed: {
    nextMonthDays() {
      return DAYS_COUNT - (this.startDayOfWeek + this.daysCount);
    }
  },
}
</script>

<style lang="scss" scoped>
.days {
  &__container {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
  }
}
</style>