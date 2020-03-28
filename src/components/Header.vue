<template>
  <header class="header">
    <div class="header__left">
      <img src="../images/ojovo.svg" alt="ojovo" />
      <p class="header__beta">Beta</p>
    </div>
    <form class="header__right">
      <button type="button" class="header__bell">
        <img src="../images/bell.svg" alt="bell" />
      </button>
      <label class="header__select-name">
        <select name="name">
          <option value="Артем">Артем</option>
        </select>
      </label>
      <button type="button" class="header__search">
        <img src="../images/search.svg" alt="bell" />
      </button>
      <label class="header__select-language">
        <select name="name" >
          <option value="Ru">Ru</option>
          <option value="En">En</option>
        </select>
      </label>
    </form>
  </header>
</template>
<script>
export default {
  name: "Header"
};
</script>

<style scoped>
.header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 60px;
}

.header__left {
  margin-top: 26px;
  display: flex;
  align-items: baseline;
}

.header__beta {
  margin-left: 9px;
  font-style: normal;
  font-weight: normal;
  font-size: 13px;
  line-height: 140%;
  margin-top: 0;
  margin-bottom: 0;
}

.header__right {
  display: flex;
  margin-top: 10px;
}

.header__bell {
  background-color: white;
  border-radius: 50%;
  width: 43px;
  height: 43px;
  margin-right: 17px;
}

.header__bell:hover {
  cursor: pointer;
}

.header__search {
  background-color: rgba(203, 215, 228, 0.4);
  border-radius: 50%;
  width: 43px;
  height: 43px;
  margin-right: 17px;
}

.header__search:hover {
  cursor: pointer;
}

.header__select-name {
  background: #ffffff;
  border-radius: 100px;
  width: 120px;
  height: 43px;
  font-style: normal;
  font-weight: bold;
  font-size: 14px;
  line-height: 17px;
  text-align: center;
  margin-right: 17px;
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
}

.header__select-name select {
  margin: 0;
  padding: 0;

  height: 100%;
  border-radius: 100px;
}

.header__select-name select:hover {
  cursor: pointer;
}

.header__select-language {
  background: rgba(203, 215, 228, 0.4);
  border-radius: 100px;
  width: 64px;
  height: 43px;
  font-style: normal;
  font-weight: bold;
  font-size: 14px;
  line-height: 17px;
  text-align: center;
  margin-right: 17px;
  display: flex;
  justify-content: center;
}

.header__select-language select {
  margin: 0;
  padding: 0;
  height: 100%;
  border-radius: 100px;
  background: rgba(203, 215, 228, 0);
}

.header__select-language select:hover {
  cursor: pointer;
}
</style>