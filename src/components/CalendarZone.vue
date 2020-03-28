<template>
<div class="calendar-zone calendar-child">
  <div class="calendar-zone__left calendar-child">
    <div 
      class="calendar-zone__period calendar-child" 
      v-bind:class="{selected: period === 'allTime'}"
      v-on:click="() => selectPeriod('allTime')"
    >
      Весь срок
    </div>
    <div 
      class="calendar-zone__period calendar-child" 
      v-bind:class="{selected: period === 'today'}"
      v-on:click="() => selectPeriod('today')"
    >
      Сегодня
    </div>
    <div 
      class="calendar-zone__period calendar-child" 
      v-bind:class="{selected: period === 'yesterday'}"
      v-on:click="() => selectPeriod('yesterday')"
    >
      Вчера
    </div>
    <div 
      class="calendar-zone__period calendar-child" 
      v-bind:class="{selected: period === 'days7'}"
      v-on:click="() => selectPeriod('days7')"
    >
      Последние 7 дней
    </div>
    <div 
      class="calendar-zone__period calendar-child" 
      v-bind:class="{selected: period === 'days30'}"
      v-on:click="() => selectPeriod('days30')"
    >
      Последние 30 дней
    </div>
    <div 
      class="calendar-zone__period calendar-child" 
      v-bind:class="{selected: period === 'Month'}"
      v-on:click="() => selectPeriod('Month')"
    >
      В этом месяце
    </div>
    <div 
      class="calendar-zone__period calendar-child" 
      v-bind:class="{selected: period === 'previousMonth'}"
      v-on:click="() => selectPeriod('previousMonth')"
    >
      Прошлый месяц
    </div>
  </div>

  <div class="calendar-zone__right calendar-child">
    <div class="select-month calendar-child">
      <button class="month__button calendar-child" v-on:click="prevMonth">
        <img src="../images/arrow__left.svg" alt="previous" class="calendar-child">
      </button>
      <p class="month calendar-child">{{month}}, {{year}}</p>
      <button class="month__button calendar-child" v-on:click="nextMonth">
        <img src="../images/arrow-right.svg" alt="next" class="calendar-child">
      </button>
    </div>
    <div class="calendar calendar-child">
      <table class="calendar__table calendar-child">
        <tr class="calendar-child calendar__row-head">
          <th class="calendar-child">пн</th>
          <th class="calendar-child">вт</th>
          <th class="calendar-child">ср</th>
          <th class="calendar-child">чт</th>
          <th class="calendar-child">пт</th>
          <th class="calendar-child">сб</th>
          <th class="calendar-child">вс</th>
        </tr>
        <tr class="calendar-child" v-for="rows in days" :key="rows.id" >
          <td 
            class="calendar-child" 
            v-for="td in rows.week" :key="td.id"
            v-bind:class="{
              checkedDate: compareDate(td, checkDay2) > 0 
                && compareDate(td, checkDay1) < 0,
              checkedDay1td: td.day === checkDay1.day 
                && td.month === checkDay1.month
                && JSON.stringify(checkDay1) !== JSON.stringify(checkDay2),
              checkedDay2td: td.day === checkDay2.day 
                && td.month === checkDay2.month
                && JSON.stringify(checkDay1) !== JSON.stringify(checkDay2),
            }"
          >
            <div 
              class="calendar-child" 
              v-bind:class="{
                'other-month': td.otherMonth,
                checkedDay1: td.day === checkDay1.day && td.month === checkDay1.month,
                checkedDay2: td.day === checkDay2.day && td.month === checkDay2.month,
              }"
              v-on:click="() => checkDay(td, td.day, td.month, td.year)"
            >
              {{td.day}}
            </div>
          </td>
        </tr>
      </table>
    </div>
    <div class="calendar-child calendar__bottom">
      <button type="button" class="cancel" v-on:click="cancel">Отмена</button>
      <button type="button" class="ok" v-on:click="ok" v-bind:class="{activateOk}">
        Обновить
      </button>
    </div>
  </div>
</div>
</template>

<script>
const date = new Date();
const getMonthName = (month) => {
  switch(month) {
    case 0:
      return "Январь";
    case 1:
      return "Февраль";
    case 2:
      return "Март";
    case 3:
      return "Апрель";
    case 4:
      return "Май";
    case 5:
      return "Июнь";
    case 6:
      return "Июль";
    case 7:
      return "Август";
    case 8:
      return "Сентябрь";
    case 9:
      return "Октябрь";
    case 10:
      return "Ноябрь";
    case 11:
      return "Декабрь";
  }
};

const getDay = (date) => {
  let day = date.getDay();

  if (day === 0) day = 7;
  return day - 1;
}

const createCalendarArray = (year, month) => {
  let mon = month;
  let daysArray = [];
  let week = [];
  let d = new Date(year, mon);
  let id = 0;
  let daysId = 0;
  let prevMonth = new Date(year, mon, 0);
  let nextMonth = new Date(year, mon + 1, 1);

  for (let i = 0; i < getDay(d); i++) {
    week.unshift({ 
      day: prevMonth.getDate() - i, 
      id: daysId, otherMonth: true,
      month: mon - 1,
      year: prevMonth.getFullYear(),
    });
    daysId++;
  }

  while (d.getMonth() === mon) {
    week.push({
      day: d.getDate(), 
      id: daysId, 
      otherMonth: false,
      month: mon,
      year: d.getFullYear()
    });
    daysId++;

    if (getDay(d) % 7 === 6) {
      daysArray.push({ week, id });
      id++;
      week = [];
    }

    d.setDate(d.getDate() + 1);
  }

  let addDay = 0;

  if (getDay(d) !== 0) {
    for (let i = getDay(d); i < 7; i++) {
      week.push({ 
        day: nextMonth.getDate() + addDay, 
        id: daysId, otherMonth: true,
        month: mon + 1,
        year: nextMonth.getFullYear(),
      });
      daysId++;
      addDay++;
    }

    daysArray.push({ week });
  }

  return daysArray;
}

export default {
  name: "CalendarZone",
  props: ['showPeriod'],
  data: function () {
    return {
      getMonth: date.getMonth(),
      period: 'today',
      month: getMonthName(date.getMonth()),
      year: date.getFullYear(),
      days: createCalendarArray(date.getFullYear(), date.getMonth()),
      checkDay1: {
        day: date.getDate(),
        month: date.getMonth(),
        year: date.getFullYear(),
      },
      checkDay2: {
        day: date.getDate(),
        month: date.getMonth(),
        year: date.getFullYear(),
      },
      compareDate: function (currentDate, comparedDate) {
        const nowDate = new Date(currentDate.year, currentDate.month, currentDate.day);
        const otherDate = new Date(comparedDate.year, comparedDate.month, comparedDate.day);

        return nowDate.getTime() - otherDate.getTime();
      },
      activateOk: false
    }
  },
  methods: {
    selectPeriod: function (period) {
      this.period = period;
      this.activateOk = true;
      let workingDate = new Date();
      const lastDayOfPreviousMonth = new Date(date.getFullYear(), date.getMonth(), 0);

      switch (period) {
        case 'today':
          workingDate = new Date();
          this.checkDay1 = {
            day: workingDate.getDate(),
            month: workingDate.getMonth(),
            year: workingDate.getFullYear(),
          };
          this.checkDay2 = {
            day: workingDate.getDate(),
            month: workingDate.getMonth(),
            year: workingDate.getFullYear(),
          };
          break;
        case 'yesterday':
          workingDate.setDate(workingDate.getDate() - 1);
          this.checkDay1 = {
            day: workingDate.getDate(),
            month: workingDate.getMonth(),
            year: workingDate.getFullYear(),
          };
          this.checkDay2 = {
            day: workingDate.getDate(),
            month: workingDate.getMonth(),
            year: workingDate.getFullYear(),
          };
          break;
        case 'allTime':
          workingDate.setDate(workingDate.getDate() - 365 * 100);
          this.checkDay2 = {
            day: workingDate.getDate(),
            month: workingDate.getMonth(),
            year: workingDate.getFullYear(),
          };
          this.checkDay1 = {
            day: date.getDate(),
            month: date.getMonth(),
            year: date.getFullYear(),
          };
          break;
        case 'days7':
          workingDate.setDate(workingDate.getDate() - 7);
          this.checkDay2 = {
            day: workingDate.getDate(),
            month: workingDate.getMonth(),
            year: workingDate.getFullYear(),
          };
          this.checkDay1 = {
            day: date.getDate(),
            month: date.getMonth(),
            year: date.getFullYear(),
          };
          break;
        case 'days30':
          workingDate.setDate(workingDate.getDate() - 30);
          this.checkDay2 = {
            day: workingDate.getDate(),
            month: workingDate.getMonth(),
            year: workingDate.getFullYear(),
          };
          this.checkDay1 = {
            day: date.getDate(),
            month: date.getMonth(),
            year: date.getFullYear(),
          };
          break;
        case 'Month':
          workingDate = new Date(date.getFullYear(), date.getMonth(), 1);
          this.checkDay2 = {
            day: workingDate.getDate(),
            month: workingDate.getMonth(),
            year: workingDate.getFullYear(),
          };
          this.checkDay1 = {
            day: date.getDate(),
            month: date.getMonth(),
            year: date.getFullYear(),
          };
          break;
        case 'previousMonth':
          workingDate = new Date(date.getFullYear(), date.getMonth() - 1, 1);
          this.checkDay2 = {
            day: workingDate.getDate(),
            month: workingDate.getMonth(),
            year: workingDate.getFullYear(),
          };
          this.checkDay1 = {
            day: lastDayOfPreviousMonth.getDate(),
            month: lastDayOfPreviousMonth.getMonth(),
            year: lastDayOfPreviousMonth.getFullYear(),
          };
          break;
      }
    },
    ok: function () {
      this.activateOk = false;
      this.showPeriod(this.checkDay2, this.checkDay1)
    },
    cancel: function () {
      this.activateOk = false;
      this.checkDay1 = {
        day: date.getDate(),
        month: date.getMonth(),
        year: date.getFullYear(),
      };
      this.checkDay2 = {
        day: date.getDate(),
        month: date.getMonth(),
        year: date.getFullYear(),
      };
    },
    prevMonth: function () {
      if (this.getMonth > 0) {
        this.getMonth--;
      } else {
        this.getMonth = 11;
        this.year--;
      }
      this.month = getMonthName(this.getMonth);
      this.days = createCalendarArray(this.year, this.getMonth);
    },
    nextMonth: function () {
      if (this.getMonth < 11) {
        this.getMonth++;
      } else {
        this.getMonth = 0;
        this.year++;
      }
      this.month = getMonthName(this.getMonth);
      this.days = createCalendarArray(this.year, this.getMonth);
    },
    checkDay: function (someDate, day, month, year) {
      this.activateOk = true;

      if (this.compareDate(someDate, this.checkDay2) > 0) {
        this.checkDay1 = {
          day,
          month,
          year,
        }
      } else {
        this.checkDay2 = {
          day,
          month,
          year,
        }
      } 
    }
  }
};
</script>

<style scoped>
  .calendar-zone {
    display: flex;
    position: absolute;
    top: 40px;
    left: -75px;
    display: none;
  }

  .calendar-zone {
    color: black;
  }

  .calendar-zone__left {
    padding: 19px 10px 30px;
    border-radius: 10px;
    background-color: white;
    margin-right: 8px;
    box-shadow: 0px 10px 40px rgba(128, 158, 191, 0.2);
    z-index: 2;
  }

  .calendar-zone__period {
    padding: 10px 0 7px 14px;
    width: 156px;
    height: 39px;
    box-sizing: border-box;
    font-family: 'PT Sans';
    font-style: normal;
    font-weight: normal;
    font-size: 15px;
    line-height: 19px;
    box-sizing: border-box;
    border-radius: 5px;
    text-align: start;
  }

  .calendar-zone__period:hover {
    border: 2px solid #EBEEF3;
  }

  .selected {
    background-color: #F0F3F8;
  }

  .calendar-zone__right {
    width: 288px;
    height: 332px;
    background-color: white;
    border-radius: 10px;
    z-index: 2;
    box-shadow: 0px 10px 40px rgba(128, 158, 191, 0.2);
    cursor: default;
  }

  .select-month {
    display: flex;
    margin: 18px 15px 15px;
    justify-content: space-between;
    align-items: center;
  }

  .month__button:hover {
    cursor: pointer;
  }

  .month__button {
    height: 24px;
    background-color: white;
  }

  .month {
    font-family: 'PT Sans';
    font-style: normal;
    font-weight: normal;
    font-size: 16px;
    line-height: 21px;
    margin: 0;
  }

  .calendar {
    width: 100%;
    height: 210px;
    background: #F3F8FD;
  }

  .calendar__bottom {
    display: flex;
    justify-content: space-between;
    margin: 10px;
  }

  .cancel {
    width: 130px;
    height: 45px;
    font-style: normal;
    font-weight: 600;
    font-size: 12px;
    line-height: 150%;
    border: 2px solid #000000;
    box-sizing: border-box;
    border-radius: 7px;
    transition: background-color 0.5s, color 0.5s;
    background-color: white;
  }

  .cancel:hover {
    background-color: black;
    color: white;
    cursor: pointer;
  }

  .ok {
    width: 130px;
    height: 45px;
    background: rgba(255, 116, 57, 0.5);
    border-radius: 7px;
    color: white;
    font-style: normal;
    font-weight: 600;
    font-size: 12px;
    line-height: 150%;
  }

  .ok:hover {
     background-color: #F16E36;
     cursor: pointer;
  }

  .calendar__table {
    width: 100%;
    height: 100%;
    border-collapse: collapse;
  }

  .calendar__row-head {
    font-style: normal;
    font-weight: bold;
    font-size: 12px;
    line-height: 15px;
    text-align: center;
  }

  td div {
    width: 28px;
    height: 28px;
    font-size: 12px;
    line-height: 15px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  td div:hover {
    cursor: pointer;
    background: #DFE9F3;
    border-radius: 50%;
  }

  .other-month {
    color: rgba(0, 0, 0, 0.2);
  }

  .checkedDay1, .checkedDay2 {
    color: white;
    background-color: #FF7439;
    border-radius: 50%;
  }

  .checkedDate {
    background: rgba(255, 116, 57, 0.2);
  }

  .checkedDay2td {
    background: linear-gradient(90deg, #F3F8FD 0%, rgba(255, 116, 57, 0.2) 60%);
  }

  .checkedDay1td {
    background: linear-gradient(90deg, rgba(255, 116, 57, 0.2) 0%, #F3F8FD 45%);
  }

  .activateOk {
    background: #FF7439;
    color: white
  }
</style>