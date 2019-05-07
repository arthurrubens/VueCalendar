<template>
  <ul class="weekNumber">
    <li
      v-for="week in weekNumbers"
      :key="week"
    >{{week}}</li>
  </ul>
</template>

<script>

export default {
  name: 'WeekNumbers',
  props: {
    shownMonth: Date
  },

  computed: {
    stShownMonth: function() {
      return this.shownMonth;
    },

    weekNumbers: function() {
      function getWeekNumber(date) {
        date.setHours(0, 0, 0, 0);
        date.setDate(date.getDate() + 3 - (date.getDay() + 6) % 7);
        var week1 = new Date(date.getFullYear(), 0, 4);
        return 1 + Math.round(((date.getTime() - week1.getTime()) / 86400000 - 3 + (week1.getDay() + 6) % 7) / 7);
      }
      var numberOfDaysInMonth = this.numberOfDaysInMonth,
          dayDate;

      var weekNumbers = [];
      for(var i=1; i<=numberOfDaysInMonth; i++) {
        dayDate = new Date(this.stShownMonth.getFullYear(), this.stShownMonth.getMonth(), i);
        if((i + 6) % 7 == 0) {
          weekNumbers.push(getWeekNumber(dayDate));
        }
      }
      return weekNumbers;
    },

    numberOfDaysInMonth: function() {
      var lastDateOfMonth = new Date(this.stShownMonth.getFullYear(), this.stShownMonth.getMonth() + 1, 0);
      return lastDateOfMonth.getDate();
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.weekNumber {
  border-right: 1px solid #6a676a;
  margin: 0;
  padding: 10px 0;
  color: $secondaryColor;
  width: calc(100% / 8);
}

.weekNumber li {
  list-style-type: none;
  display: inline-block;
  width: 100%;
  text-align: center;
  margin-bottom: 5px;
  padding: 3px;
  font-size:12px;
  color: $secondaryColor;
}
</style>
