<template>
  <div class="dropDown">
    <button class="dropButton">{{currentMonthName}}</button>
    <ul class="dropDownContent">
        <li
            v-for="(month, index) in stMonths"
            :key="month.title"
        >
          <a @click="onMonthClick(index)" href="#">{{month.title}}</a>
        </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "MonthDropDown",
  props: {
    shownMonth: Date
  },

  data: function() {
      return {
        stMonths: [{
            title: "JAN"
        }, {
            title: "FEB"
        }, {
            title: "MAR"
        }, {
            title: "APR"
        }, {
            title: "MAY"
        }, {
            title: "JUN"
        }, {
            title: "JUL"
        }, {
            title: "AUG"
        }, {
            title: "SEP"
        }, {
            title: "OCT"
        }, {
            title: "NOV"
        }, {
            title: "DEC"
        }]
      };
  },

  computed: {
    stShownMonth: function() {
      return this.shownMonth;
    },

    currentMonthName: function() {
      var month = this.stShownMonth.toLocaleString("en-us", { month: "long" });
      return month;
    }
  },

  methods: {
    onMonthClick: function(monthNumber) {
      this.showDropDown = false;
      this.$emit('monthSelected', monthNumber);
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
  color: $monthColor;
  font-size: 2em;
  border: none;
  cursor: pointer;
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
