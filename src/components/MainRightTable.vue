<template>
  <table class="main__right-table">
    <thead class="row-head">
      <tr class="table__tr">
        <td>
          <input type="radio" class="table__checkbox" />
        </td>
        <td>
          <div class="table__users">Пользователи</div>
        </td>
        <td class="hide-on-small-screen">
          <div class="table__registration">Дата регистрации</div>
        </td>
        <td>
          <div class="table__last-use">Последняя активность</div>
        </td>
        <td>
          <div class="table__last-action">Последнее действие</div>
        </td>
        <td>
          <div class="table__product">Продукт</div>
        </td>
        <td>
          <label class="table__lable">
            Отобразить&nbsp;
            <select name="amount" v-on:change = "e => changeAmountUsers(e)">
              <option value="5">5</option>
              <option value="10">10</option>
              <option value="15" selected>15</option>
              <option value="20">20</option>
            </select>
          </label>
        </td>
      </tr>
    </thead>
    <div class="table__hr"></div>

    <tbody class="tbody">
      <tr v-for="row in data" :key="row.id" class="table__tr">
        <td>
          <input type="radio" class="table__checkbox" />
        </td>
        <td class="table__users">
          <div class="table-body__users"> 
            <img v-if="row.id === 7" src="../images/lock.svg" alt="locked">
            User{{row.id}} 
          </div>
          <div class="table-body__email">{{row.email}} </div>
        </td>
        <td v-bind:class="{lock: row.id === 7}">
          <div class="table__registration table__date hide-on-small-screen">
            {{row.date[1]}} {{row.date[2]}}, {{row.date[0]}}
          </div>
        </td>
        <td v-bind:class="{lock: row.id === 7}">
          <div class="table__last-use table__date">
            {{row.date[1]}} {{row.date[2]}}, {{row.date[0]}}
          </div>
        </td>
        <td v-bind:class="{lock: row.id === 7}">
          <div class="table__last-action table__text">view_landing_course1</div>
        </td>
        <td v-bind:class="{lock: row.id === 7}">
          <p class="table__product table__text">Как наладить отношения</p>
        </td>
        <td>
          <label class="table__lable">
            <button class="table__edit table__button">
              <img src="../images/pencill.svg" alt="edit">
            </button>
            <button class="table__button">
              <img src="../images/delete.svg" alt="delete">
            </button>
          </label>
        </td>
      </tr>
    </tbody>
  </table>
</template>
<script>
import users from "../data/users.json";

const data = users.data.map(user => ({
  ...user,
  date: user.created_at
    .split(" ")[0]
    .split("-")
    .map((day, index, array) => {
      if (index === 1 && array[1] === "01") return "январь";
      if (index === 1 && array[1] === "02") return "февраль";
      if (index === 1 && array[1] === "03") return "март";
      if (index === 1 && array[1] === "04") return "апрель";
      if (index === 1 && array[1] === "05") return "май";
      if (index === 1 && array[1] === "06") return "июнь";
      if (index === 1 && array[1] === "07") return "июль";
      if (index === 1 && array[1] === "08") return "август";
      if (index === 1 && array[1] === "09") return "сентябрь";
      if (index === 1 && array[1] === "10") return "октябрь";
      if (index === 1 && array[1] === "11") return "нояобрь";
      if (index === 1 && array[1] === "12") return "декабрь";
      if (index !== 1) return day;
    }),
}));

export default {
  name: "MainRightTable",
  data: function () {
    return {
      amountUsers: 15,
      data: data.filter((row, index) => index < 15),
    }
  },
  methods: {
    changeAmountUsers: function (e) {
      this.data = data.filter((row, index) => index < e.target.value);
    }
  }
};
</script>
<style scoped>
.main__right-table {
  padding: 20px 24px 20px 32px;
  display: flex;
  flex-direction: column;
  background-color: white;
  border-radius: 10px;
  width: 100%;
}

.row-head {
  display: flex;
  font-weight: bold;
  font-size: 13px;
  line-height: 130%;
  justify-content: space-between;
  align-items: center;
}

.row-head div {
  display: flex;
  flex-wrap: wrap;
  margin-right: 10px;
}

.table__checkbox {
  border-radius: 50%;
  margin-right: 38px;
  border: 2px solid rgba(131, 142, 157, 0.3);
  box-sizing: border-box;
  width: 26px;
  height: 26px;
}

.table__users {
  width: 189px;
  overflow: hidden;
}

.table__registration {
  width: 137px;
}

.table__last-use {
  width: 166px;
  text-align: start;
}

.table__last-action {
  width: 150px;
  overflow: hidden;
  margin-right: 10px;
}

.table__product {
  width: 168px;
  overflow: hidden;
  margin-right: 10px;
  text-align: start;
  white-space: nowrap;
}

.table__lable {
  font-style: normal;
  font-weight: 500;
  font-size: 13px;
  line-height: 130%;
  text-align: center;
  width: 120px;
  display: flex;
  justify-content: flex-end;
}

.table__lable select {
  border-radius: 10px;
}

.table__hr {
  height: 1px;
  background-color: #e7ecf1;
  margin-bottom: 21px;
  margin-top: 16px;
}

.table-body__users {
  font-style: normal;
  font-weight: 500;
  font-size: 15px;
  line-height: 130%;
  margin-top: 13px;
  display: flex;
}

.table-body__users img {
  margin-right: 7px;
}

.table-body__email {
  font-style: normal;
  font-weight: 300;
  font-size: 13px;
  line-height: 130%;
  max-width: 189px;
  overflow: hidden;
  margin-right: 10px;
  position: relative;
}

.table__date {
  font-style: normal;
  font-weight: 500;
  font-size: 15px;
  line-height: 130%;
  margin-right: 10px;
}

.table__text {
  font-style: normal;
  font-weight: 500;
  font-size: 15px;
  line-height: 130%;
  position: relative;
}

.table__edit {
  margin-right: 13px;
}

.table__button {
  background-color: white;
}

.table__button:hover {
  cursor: pointer;
}

.table__tr {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.table__text::after {
  content: '';
  position: absolute;
  right: 0; top: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(to right, rgba(255, 255, 255, 0.2) 80%, white 100%);
}

.table-body__email::after {
  content: '';
  position: absolute;
  right: 0; top: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(to right, rgba(255, 255, 255, 0.2) 80%, white 100%);
}

.lock {
  color: grey;
}

@media(max-width: 1450px) {
  .table__users {
    width: 8vw;
  }

  .table__registration {
    width: 8vw;
  }

  .table-body__users {
    width: 8vw;
  }

  .table__last-use {
    width: 8vw;
  }

  .table__last-action {
    width: 8vw;
  }

  .table__product {
    width: 8vw;
  }

  .table__product {
    width: 8vw;
  }
}

@media(max-width: 1150px) {
  .table__users {
    width: 10vw;
  }

  .table__registration {
    width: 9vw;
  }

  .table-body__users {
    width: 10vw;
  }

  .table__last-use {
    width: 9vw;
  }

  .table__last-action {
    width: 9vw;
  }

  .table__product {
    width: 9vw;
  }

  .table__product {
    width: 9vw;
  }

  .table__checkbox {
    margin-right: 10px;
  }

  .main__right-table {
    width: 90%;
  }

  .hide-on-small-screen {
    display: none;
  }
}
</style>