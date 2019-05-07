<template>
  <div class="calendar">
    <Header
      :shownMonth="stShownMonth"
      @ShownMonthChange="onShownMonthChange"
    />
    <div class="calendarBody">
      <WeekDays/>
        <div class="rowLayout">
          <WeekNumbers :shownMonth="stShownMonth"/>
          <MonthDays
            :shownMonth="stShownMonth"
            :selectedDate="stSelectedDate"
            :events="stEvents"
            @SelectedDayChange="onSelectedDayChange"
          />
        </div>
      </div>
    </div>
</template>

<script>
import Header from './Header'
import WeekDays from './WeekDays';
import WeekNumbers from './WeekNumbers';
import MonthDays from './MonthDays';

export default {
  name: 'Calendar',
  components: {
    Header,
    WeekNumbers,
    WeekDays,
    MonthDays
  },
  props: {
    events: Array,
    selectedDate: Date,
    shownMonth: Date
  },

  data: function() {
    return {
      stEvents: this.events,
      stSelectedDate: this.selectedDate,
      stShownMonth: this.shownMonth,
    };
  },

  methods: {
    onShownMonthChange: function(shownMonth) {
      this.stShownMonth = shownMonth;
    },

    onSelectedDayChange: function(selectedDay) {
      this.stSelectedDate = new Date(selectedDay);
      this.$emit('SelectedDayChange', this.stSelectedDate);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
* {
    font-family: Verdana, sans-serif;
    box-sizing: border-box;
}

ul {
    list-style-type: none;
}

li {
    border: 1px solid rgba(85, 85, 85, 0.2);
}

a:link,
a:visited,
a:hover,
a:active,
a:focus {
    text-decoration: none;
    color: inherit;
}

*:focus {
    outline: none;
}

.calendar {
  position: relative;
  background-color: $primaryBackgroundColor;
  border-radius: 5px;
}

.rowLayout {
  display: flex;
  flex-direction: row;
  padding-bottom: 5px;
}
</style>
