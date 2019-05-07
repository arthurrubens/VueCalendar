<template>
  <ul class="days">
      <DayCell
        v-for="day in monthDays"
          :key="day.dayDate.toDateString()"
          :dayNumber="day.dayNumber"
          :dayDate="day.dayDate"
          :disabled="day.disabled"
          :isSelected="day.isSelected"
          :eventDescription="day.eventDescription"
          @DayClicked="dayClick(day.dayDate)"
      />
  </ul>
</template>

<script>
import DayCell from './DayCell';

export default {
  name: 'MonthDays',
  components: {
    DayCell
  },
  props: {
    events: Array,
    selectedDate: Date,
    shownMonth: Date
  },

  data: function() {
    return {
      stShownMonth: this.shownMonth,
      stSelectedDate: this.selectedDate
    }
  },
  watch: {
    shownMonth: function(newDate) {
      this.stShownMonth = newDate;
    }
  },

  computed: {
    monthDays: function() {
      var monthDays = [],
          monthIndex = this.stShownMonth.getMonth(),
          beginOffset = new Date(this.stShownMonth.getFullYear(), monthIndex, -1).getDay();

      beginOffset = beginOffset == 6 ? -1 : beginOffset;
      for(var i=0; i<35; i++) {
        var dayDate = new Date(this.stShownMonth.getFullYear(), monthIndex, i - beginOffset),
            disabled = dayDate.getMonth() != this.stShownMonth.getMonth();
        monthDays.push({
          dayNumber: dayDate.getDate(),
          dayDate: dayDate,
          disabled: disabled,
          isSelected: this.stSelectedDate.toDateString() == dayDate.toDateString(),
          eventDescription: this.getEventDescription(dayDate)
        });
      }
      return monthDays;
    },

    numberOfDaysInMonth: function() {
      var lastDateOfMonth = new Date(this.shownMonth.getFullYear(), this.shownMonth.getMonth() + 1, 0);
      return lastDateOfMonth.getDate();
    }
  },
  
  methods: {
    dayClick: function(clickedDate) {
      this.stSelectedDate = new Date(clickedDate);
      this.$emit('SelectedDayChange', this.stSelectedDate);
    },

    getEventDescription: function(date) {
      var eventDescription = '',
          dateString = date.toDateString();
      for(let i=0; i<this.events.length; i++) {
        if(this.events[i].date.toDateString() == date.toDateString()) {
          eventDescription = this.events[i].title;
          break;
        }
      };
      return eventDescription;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.days {
  list-style-type: none;
  margin: 0;
  padding: 10px 0;
  width: calc(700% / 8);
}
</style>
