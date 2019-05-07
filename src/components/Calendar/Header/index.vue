<template>
  <div class="headerWrapper">
    <div class="firstSubHeader">
      <span class="prev"><a href="#" @click="prevMonthClick">&#10094;</a></span>
      <span class="today"><a href="#" @click="nextTodayClick">Today</a></span>
      <span class="next"><a href="#" @click="nextMonthClick">&#10095;</a></span>
    </div>
    <div class="secondSubHeader">
      <MonthDropDown
        :shownMonth="stShownMonth"
        class="currentMonth"
        @monthSelected="onMonthSelected"
      />
      <YearDropDown
        :shownMonth="stShownMonth"
        class="currentYear"
        @YearSelected="onYearSelected"
      />
    </div>
  </div>
</template>

<script>

import MonthDropDown from './MonthDropDown';
import YearDropDown from './YearDropDown';

export default {
  name: 'Header',
  components: {
    MonthDropDown,
    YearDropDown
  },
  props: {
    shownMonth: Date
  },

  computed: {
    stShownMonth: function() {
      return this.shownMonth;
    },

    currentMonthName: function() {
      var month = this.stShownMonth.toLocaleString('en-us', { month: 'long' });
      return month;
    },

    currentYear: function() {
      var fullYear = this.stShownMonth.getFullYear();
      return fullYear;
    }
  },
  
  methods: {
    onMonthSelected: function(monthNumber) {
      var shownMonth = new Date(this.stShownMonth.getFullYear(), monthNumber, 1);
      this.$emit('ShownMonthChange', shownMonth);
    },

    onYearSelected: function(year) {
      var shownMonth = new Date(year, this.stShownMonth.getMonth(), 1);
      this.$emit('ShownMonthChange', shownMonth);
    },

    nextTodayClick: function() {
      var shownMonth = new Date();
      this.$emit('ShownMonthChange', shownMonth);
    },

    prevMonthClick: function() {
      var shownMonth = new Date(this.stShownMonth.getFullYear(), this.stShownMonth.getMonth() - 1, 1);
      this.$emit('ShownMonthChange', shownMonth);
    },

    nextMonthClick: function() {
      var shownMonth = new Date(this.stShownMonth.getFullYear(), this.stShownMonth.getMonth() + 1, 1);
      this.$emit('ShownMonthChange', shownMonth);
    },

    dayClick: function(clickedDate) {
      this.stSelectedDate = new Date(clickedDate);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.headerWrapper {
  padding: 10px 25px 10px 20px;
  width: 100%;
  text-align: center;
}

.firstSubHeader {
  margin-bottom: 10px;
}

.secondSubHeader {
  
}

.firstSubHeader .prev {
  position: absolute;
  left: 10px;
  color: #fff;
}

.firstSubHeader .next {
  position: absolute;
  right: 10px;
  color: #fff;
}

.firstSubHeader .today {
  color: #fff;
}
</style>
