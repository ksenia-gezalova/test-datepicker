<template>
  <div class="header">
    <div class="header__date">
      <span class="header__arrow" @click="goLast">&#60;</span>
      <div class="header__title">
        {{currentDate.month}} 
        <input v-if="isYearEdit" v-model="currentYear" 
          @keyup.enter="stopEditYear" @blur="stopEditYear" ref="input" />
        <span v-else @click="editYear">{{currentDate.year}}</span>
      </div>
      <span class="header__arrow" @click="goNext">&#62;</span>
    </div>
    <div class="header__week">
      <div class="header__item" v-for="item in week" :key="item">
        {{item}}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DatepickerHeader',
  props: {
    currentDate: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      week: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
      isYearEdit: false,
      yearBuffer: null,
    }
  },
  computed: {
    currentYear: {
      get() {
        return this.currentDate.year;
      },
      set(value) {
        this.yearBuffer = value;
      }
    }
  },
  methods: {
    goLast() {
      this.$emit('goLast');
    },
    goNext() {
      this.$emit('goNext');
    },
    editYear() {
      this.isYearEdit = true;
      setTimeout(() => this.$refs.input.focus(), 100);
    },
    stopEditYear() {    
      this.$emit('setCurrentYear', this.yearBuffer);
      this.yearBuffer = null;

      this.isYearEdit = false;
    }
  }
}
</script>

<style lang="scss" scoped>
.header {
  min-height: 40px;
  width: 310px;
  background-color: #fff;
  border-bottom: 1px solid rgba(#000, 0.1);

  &__date {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  &__arrow {
    padding: 10px;
    cursor: pointer;
  }

  &__title {
    input {
      width: 40px;
      text-align: center;
      border: 1px solid rgb(59, 114, 59);
      outline-color: rgb(59, 114, 59);
      outline-width: 1px;

      &:focus {
        border: none;
      }
    }
  }

  &__week {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
  }

  &__item {
    text-align: center;
    color: rgb(187, 183, 183);
  }
}

</style>