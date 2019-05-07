<template>
    <ul class="weekDays">
      <li
        v-for="weekDay in stWeekDays"
        :key="weekDay.id"
      >{{weekDay.title}}</li>
    </ul>
</template>

<script>
export default {
  name: 'WeekDays',

  data: function() {
    return {
      stWeekDays: [{
        id: 'wn',
        title: "WN"
      }, {
        id: 'mon',
        title: "MON"
      }, {
        id: 'tue',
        title: "TUE"
      }, {
        id: 'wed',
        title: "WED"
      }, {
        id: 'thu',
        title: "THU"
      }, {
        id: 'fri',
        title: "FRI"
      }, {
        id: 'sat',
        title: "SAT"
      }, {
        id: 'sun',
        title: "SUN"
      }]
    };
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.weekDays {
  list-style-type: none;
  margin: 0;
  padding: 10px 0 5px 0;
}

.weekDays li {
  display: inline-block;
  width: calc(100% / 8);
  color: $secondaryColor;
  text-align: center;
  padding: 3px;
}
</style>
