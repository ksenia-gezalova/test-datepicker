<template>
  <div :class="dayClass">
    <span class="day__month" v-if="(day == 1) && nextMonthLabel">{{nextMonthLabel}}</span> {{day}}
  </div>
</template>

<script>
export default {
  name: 'DatepickerDay',
  props: {
    isNextMonth: {
      type: Boolean,
      default: false
    },
    day: {
      type: [Number, String],
      required: true
    },
    nextMonthLabel: {
      type: String,
      required: false
    }
  }, 
  computed: {
    dayClass() {
      return {
        day: true,
        'day--out': this.isNextMonth
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.day {
  position: relative;
  padding: 12px 5px;
  text-align: center;
  background: #fff;
  cursor: pointer;
  transition: .3s;

  &:hover {
    background: rgb(59, 114, 59);
    color: #fff;
  }

  &--out {
    background: #eee;
  }

  &__month {
    position: absolute;
    font-size: 10px;
    top: 0;
    left: 13px;
  }
}
</style>