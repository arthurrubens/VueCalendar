<template>
  <div class="dropDown">
    <button class="dropButton currentYearColor">{{selectedYear}}</button>
    <ul class="dropDownContent">
      <li class="ulHeader">
        <span class="prev"><a href="#" @click="prevYearRangeClick">&#10094;</a></span>
        <span class="today">{{yearRangeBegin}} - {{yearRangeEnd}}</span>
        <span class="next"><a href="#" @click="nextYearRangeClick">&#10095;</a></span>
      </li>
        <li
            v-for="year in years"
            :key="year"
        >
          <a @click="onYearClick(year)" href="#" ><span :class="{'currentYearColor': year == selectedYear}">{{year}}</span></a>
        </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "YearDropDown",
  props: {
    shownMonth: Date
  },

  data: function() {
    return {
      selectedYear: this.shownMonth.getFullYear(),
      currentYear: this.shownMonth.getFullYear(),
      radius: 4
    }
  },

  watch: {
    shownMonth: function(newDate) {
      this.selectedYear = newDate.getFullYear();
      this.currentYear = newDate.getFullYear();
    }
  },

  computed: {
    years: function() {
      var years = [];
      for(let i=this.yearRangeBegin; i<=this.yearRangeEnd; i++) {
        years.push(i);
      }
      return years;
    },

    yearRangeBegin: function() {
      var fullYear = this.currentYear;
      return this.currentYear - this.radius;
    },

    yearRangeEnd: function() {
      var fullYear = this.currentYear;
      return this.currentYear + this.radius;
    }
  },

  methods: {
    onYearClick: function(year) {
      this.showDropDown = false;
      this.selectedYear = year;
      this.$emit('YearSelected', year);
    },
    prevYearRangeClick: function() {
      this.currentYear -= 2*this.radius;
    },
    nextYearRangeClick: function() {
      this.currentYear += 2*this.radius;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.dropDown {
  position: relative;
  display: inline-block;
}

.dropButton {
  background-color: transparent;
  font-size: 2em;
  border: none;
  cursor: pointer;
}

.currentYearColor {
  color: $yearColor;
}

.dropDownContent {
  display: none;
  position: absolute;
  margin: auto;
  top: calc(2em + 8px);
  right: calc(50% - 125px);;
  background-color: $secondaryColor;
  color: #fff;
  box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
  border-radius: 5px;
  width: 250px;
  list-style-type: none;
  padding: 0;
  z-index: 1;
}

.dropDownContent a,
.dropdown:hover{
  display: block;
}

.dropDownContent:after, .dropDownContent:before {
	bottom: 100%;
	left: 50%;
	border: solid transparent;
	content: " ";
	height: 0;
	width: 0;
	position: absolute;
	pointer-events: none;
}

.dropDownContent:after {
	border-bottom-color: $secondaryColor;
	border-width: 5px;
	margin-left: -5px;
}
.dropDownContent:before {
	border-bottom-color: $secondaryColor;
	border-width: 5px;
	margin-left: -5px;
}

.dropDownContent li.ulHeader {
  width: 100%;
  color: #fff;
}

.dropDownContent li.ulHeader .prev {
  position: absolute;
  left: 5px;
}

.dropDownContent li.ulHeader .next {
  position: absolute;
  right: 5px;
}

.dropDownContent li {
  display: inline-block;
  width: calc(100% / 3);
  color: $secondaryColor;
  text-align: center;
  padding: 3px;
}

.dropDownContent li a {
  color: #fff;
  margin: 2px;
  text-decoration: none;
  display: block;
}

.dropDownContent a:hover {
  background-color: $secondaryColor;
}

.dropDown:hover .dropDownContent {
  display: block;
}

.dropDown:hover .dropButton {
  background-color: transparent;
}
</style>
