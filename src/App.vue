<template>
  <div id="app">
    <Calendar
      :selectedDate="selectedDate"
      :shownMonth="shownMonth"
      :events="events"
      @SelectedDayChange="onSelectedDayChange"
    />
    <h1>{{selectedDate.toDateString()}}</h1>
  </div>
</template>

<script>
import Calendar from './components/Calendar'

export default {
  name: 'app',
  components: {
    Calendar
  },
  data: function() {
    return {
      selectedDate: new Date(new Date().setHours(0, 0, 0)),
      shownMonth: new Date(),
      events:[{
        date: new Date(),
        title: "Today"
      }, {
        date: new Date('1 January, 2019 00:00:00'),
        title: "New Year's Day"
      }, {
        date: new Date('6 January, 2019 00:00:00'),
        title: "Epiphany"
      }, {
        date: new Date('8 March, 2019 00:00:00'),
        title: "Women's Day"
      }, {
        date: new Date('15 March, 2019 00:00:00'),
        title: "My Birthday"
      }, {
        date: new Date('20 April, 2019 00:00:00'),
        title: "My Birthday"
      }, {
        date: new Date('1 May, 2019 00:00:00'),
        title: "Labour Day"
      }, {
        date: new Date('8 August, 2019 00:00:00'),
        title: "Peace Festival"
      }, {
        date: new Date('15 August, 2019 00:00:00'),
        title: "Assumption Day"
      }, {
        date: new Date('20 September, 2019 00:00:00'),
        title: "World Children's Day"
      }, {
        date: new Date('3 October, 2019 00:00:00'),
        title: "German Unity Day"
      }, {
        date: new Date('31 October, 2019 00:00:00'),
        title: "Reformation Day"
      }, {
        date: new Date('1 November, 2019 00:00:00'),
        title: "All Saints"
      }, {
        date: new Date('25 December, 2019 00:00:00'),
        title: "Christmas Day"
      }, {
        date: new Date('26 December, 2019 00:00:00'),
        title: "Boxing Day"
      }]
    }
  },

  methods: {
    onSelectedDayChange: function(newSelectedDate) {
      this.selectedDate = newSelectedDate;
    }
  }
}
</script>

<style lang="scss" scoped>
#app {
  width: 400px;
}
</style>
