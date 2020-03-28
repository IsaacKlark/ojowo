<template>
  <section class="main__right-head">
    <div class="main__right-head-wrapper">
      <div class="main__right-head-left">
        <button
          class="label__calendar calendar-btn calendar-child"
          v-on:mouseover="hoveredCalendar"
          v-on:mouseleave="notHoveredCalendar"
          v-on:click="showCalendarZoneFunc"
        >
          <img
            v-if="!hoveredCalendarBtn"
            src="../images/calendar.svg"
            alt="calendar"
            class="left-img calendar-child"
          />
          <img
            v-else
            src="../images/calendar-orange.svg"
            alt="calendar"
            class="left-img calendar-child"
          />
          <div type="text" class="calendar-input input calendar-child">За 1 день</div>
          <img
            v-if="!hoveredCalendarBtn"
            src="../images/arrow-bottom.svg"
            alt="select"
            class="arrow-img calendar-child"
          />
          <img
            v-else
            src="../images/arrow-bottom-orange.svg"
            alt="select"
            class="arrow-img calendar-child"
          />

          <CalendarZone v-bind:showPeriod="showPeriod"/>
        </button>

        <button
          class="label__calendar calendar-btn"
          v-on:mouseover="hoveredFilter"
          v-on:mouseleave="notHoveredFilter"
        >
          <img v-if="!hoveredFilterBtn" src="../images/filter.svg" alt="filter" class="left-img" />
          <img v-else src="../images/filter-orange.svg" alt="filter" class="left-img" />
          <div type="text" class="filter-input input">Фильтр</div>
          <img
            v-if="!hoveredFilterBtn"
            src="../images/arrow-bottom.svg"
            alt="select"
            class="arrow-img"
          />
          <img v-else src="../images/arrow-bottom-orange.svg" alt="select" class="arrow-img" />
        </button>
      </div>

      <div class="main__right-head-right">
        <button type="button" class="load">Выгрузить</button>
        <button type="button" class="add-contacts">Добавить контакты</button>
      </div>
    </div>
    <div v-if="activatedPeriod" class="hr"></div>
    <div v-if="activatedPeriod" class="showPeriod">
      {{period}}
      <button type="button" v-on:click="hidePeriod">
        <img src="../images/grayCross.svg" alt="close" />
      </button>
    </div>
  </section>
</template>

<script>
import CalendarZone from "./CalendarZone";
export default {
  name: "MainRightHead",
  components: {
    CalendarZone
  },
  data: function() {
    return {
      hoveredCalendarBtn: false,
      hoveredFilterBtn: false,
      activatedPeriod: false,
      period: ""
    };
  },
  methods: {
    hoveredCalendar: function() {
      this.hoveredCalendarBtn = true;
    },
    notHoveredCalendar: function() {
      this.hoveredCalendarBtn = false;
    },
    hoveredFilter: function() {
      this.hoveredFilterBtn = true;
    },
    notHoveredFilter: function() {
      this.hoveredFilterBtn = false;
    },
    showCalendarZoneFunc: function() {
      document.querySelector(".calendar-zone").style.display = "flex";
    },
    hidePeriod: function() {
      this.activatedPeriod = false;
    },
    showPeriod: function(fistDate, secondDate) {
      this.activatedPeriod = true;
      let shortDateName1 = getShortName(fistDate.month);
      let shortDateName2 = getShortName(secondDate.month);

      function getShortName(month) {
        switch (month) {
          case 0:
            return "янв";
          case 1:
            return "фев";
          case 2:
            return "мар";
          case 3:
            return "апрел";
          case 4:
            return "май";
          case 5:
            return "июн";
          case 6:
            return "июл";
          case 7:
            return "авг";
          case 8:
            return "Сентябрь";
          case 9:
            return "Октябрь";
          case 10:
            return "Ноябрь";
          case 11:
            return "Декабрь";
        }
      }

      this.period = `${fistDate.day} ${shortDateName1} - ${secondDate.day} ${shortDateName2} ${secondDate.year}г.`;
    }
  }
};
</script>

<style scoped>
.main__right-head {
  width: 100%;
  padding: 20px 21px 20px 35px;
  background-color: white;
  margin-bottom: 10px;
  border-radius: 10px;
  margin-right: 21px;
}

.main__right-head-wrapper {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.main__right-head-left {
  display: flex;
}

.label__calendar {
  display: flex;
  align-items: center;
  margin-right: 44px;
}

.left-img {
  margin-right: 23px;
}

.arrow-img {
  margin-left: 8px;
}

.calendar-input {
  width: 73px;
}

.filter-input {
  width: 62px;
}

.input {
  font-style: normal;
  font-weight: 500;
  font-size: 15px;
  line-height: 130%;
}

.main__right-head-right {
  display: flex;
}

.load {
  font-style: normal;
  font-weight: bold;
  font-size: 14px;
  line-height: 150%;
  width: 120px;
  height: 45px;
  border: 2px solid #000000;
  box-sizing: border-box;
  border-radius: 7px;
  transition: color 0.8s, background-color 0.8s;
  margin-right: 11px;
}

.load:hover {
  cursor: pointer;
  background-color: black;
  color: white;
}

.add-contacts {
  background: #ff7439;
  border-radius: 7px;
  color: white;
  font-weight: bold;
  font-size: 14px;
  line-height: 150%;
  width: 199px;
  height: 45px;
  transition: color 0.8s, background-color 0.8s;
}

.add-contacts:hover {
  background: #f16e36;
  cursor: pointer;
}

.calendar-btn {
  background-color: white;
  position: relative;
}

.calendar-btn:hover {
  color: #ff7439;
  cursor: pointer;
}

.hr {
  width: 100%;
  height: 1px;
  background: #e7ecf1;
  margin-top: 30px;
  margin-bottom: 12px;
}

.showPeriod {
  font-family: "PT Sans";
  font-style: normal;
  font-weight: bold;
  font-size: 15px;
  line-height: 150%;
  color: #ffffff;
  background: #586375;
  border-radius: 100px;
  display: flex;
  justify-content: space-around;
  width: 223px;
  height: 41px;
  align-items: center;
}

.showPeriod button {
  width: 27px;
  height: 27px;
  background: #586375;
}

.showPeriod button:hover {
  cursor: pointer;
}

@media (max-width: 1150px) {
  .label__calendar {
    margin-right: 10px;
  }

  .main__right-head {
    width: 90%;
  }

  .load {
    width: 100px;
  }

  .add-contacts {
    width: 150px;
  }
}
</style>