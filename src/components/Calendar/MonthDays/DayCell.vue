<template>
    <li
      :class="[{event: isEvent}, 'tooltip']"
    >
      <a
        :href="'#' + dayDate"
        @click="onDayClick(dayDate)"
        v-if="!disabled"
      >
          <div :class="[{selected: isSelected}, 'dayNumberContainer']">{{dayNumber}}</div>
      </a>
      <div v-else class="dayNumberContainer dayNumberDisabled">{{dayNumber}}</div>
      <span v-if="isEvent" class="tooltiptext">{{eventDescription}}</span>
  </li>
</template>

<script>
export default {
  name: 'DayCell',
  props: {
    dayNumber: Number,
    dayDate: Date,
    disabled: Boolean,
    isSelected: Boolean,
    eventDescription: String
  },
  
  computed: {
    isEvent: function() {
      return !!this.eventDescription.length;
    }
  },

  methods: {
    onDayClick: function(clickedDate) {
      this.$emit('DayClicked', clickedDate);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.days li {
  list-style-type: none;
  display: inline-block;
  width: calc(100% / 7);
  text-align: center;
  margin-bottom: 5px;
  font-size:12px;
  color: #fff;
}

.dayNumberContainer {
  padding: 3px;
}

.dayNumberDisabled {
  color: $secondaryColor;
}

.selected {
  display: block;
  background-color: #4492f7;
  border-radius: 1em;
  width: 2em;
  margin: 0 auto;
}

.event {
  background-color: $eventsColor;
  border-radius: 1em;
}

.tooltip {
  position: relative;
  display: inline-block;
}

.tooltip .tooltiptext {
  visibility: hidden;
  width: 120px;
  background-color: $secondaryColor;
  color: #fff;
  text-align: center;
  border-radius: 6px;
  padding: 5px 0;
  position: absolute;
  z-index: 1;
  bottom: 125%;
  left: 50%;
  margin-left: -60px;
  opacity: 0;
  transition: opacity 0.3s;
}

.tooltip .tooltiptext::after {
  content: "";
  position: absolute;
  top: 100%;
  left: 50%;
  margin-left: -5px;
  border-width: 5px;
  border-style: solid;
  border-color: #555 transparent transparent transparent;
}

.tooltip:hover .tooltiptext {
  visibility: visible;
  opacity: 1;
}

</style>
