<template>
  <article class="main__left">
    <label class="main__bread">
      <select name="main__bread">
        <option value="expert">
          expert
        </option>
      </select>
      <img src="../images/bread.svg" alt="">
    </label>

    <section class="main__left-main">
      <div 
        class="main__card"
        v-bind:class="{selected: selectedCard === 'analytics'}"
        v-on:click="selectedCard = 'analytics'"
      >
        <img 
          v-if="selectedCard === 'analytics'" 
          src="../images/analytic-orange.svg" 
          alt="analytic"
        >
        <img 
          v-else
          src="../images/analytic.svg" 
          alt="analytic"
        >
        <p>Аналитика</p>
      </div>
      <div 
        class="main__card"
        v-bind:class="{selected: selectedCard === 'product'}"
        v-on:click="selectedCard = 'product'"
      >
        <img 
          v-if="selectedCard === 'product'" 
          src="../images/product-orange.svg" 
          alt="analytic"
        >
        <img 
          v-else
          src="../images/product.svg" 
          alt="analytic"
        >
        <p>Продукт</p>
      </div>
      <div 
        class="main__card" 
        v-bind:class="{selected: selectedCard === 'users'}"
        v-on:click="selectedCard = 'users'"
      >
        <img 
          v-if="selectedCard === 'users'" 
          src="../images/users-orange.svg" 
          alt="analytic"
        >
        <img 
          v-else
          src="../images/users.svg" 
          alt="analytic"
        >
        <p>Пользователи</p>
      </div>
      <div 
        class="main__card"
        v-bind:class="{selected: selectedCard === 'constructor'}"
        v-on:click="selectedCard = 'constructor'"
      >
        <img 
          v-if="selectedCard === 'constructor'" 
          src="../images/constructor-orange.svg" 
          alt="analytic"
        >
        <img 
          v-else
          src="../images/constructor.svg" 
          alt="analytic"
        >
        <p>Конструктор сайта</p>
      </div>
      <div class="main__card"
        v-bind:class="{selected: selectedCard === 'translation'}"
        v-on:click="selectedCard = 'translation'"
      >
        <img 
          v-if="selectedCard === 'translation'" 
          src="../images/translation-orange.svg" 
          alt="analytic"
        >
        <img 
          v-else
          src="../images/translation.svg" 
          alt="analytic"
        >
        <p>Трансляции</p>
      </div>
      <div 
        class="main__card"
        v-bind:class="{selected: selectedCard === 'messages'}"
        v-on:click="selectedCard = 'messages'"
      >
        <img 
          v-if="selectedCard === 'messages'" 
          src="../images/messages-orange.svg" 
          alt="analytic"
        >
        <img 
          v-else
          src="../images/messages.svg" 
          alt="analytic"
        >
        <p>Рассылки</p>
      </div>
      <div 
        class="main__card"
        v-bind:class="{selected: selectedCard === 'marketing'}"
        v-on:click="selectedCard = 'marketing'"
      >
        <img 
          v-if="selectedCard === 'marketing'" 
          src="../images/marketing-orange.svg" 
          alt="analytic"
        >
        <img 
          v-else
          src="../images/marketing.svg" 
          alt="analytic"
        >
        <p>Маркетинг</p>
      </div>
      <div 
        class="main__card"
        v-bind:class="{selected: selectedCard === 'pay'}"
        v-on:click="selectedCard = 'pay'"
      >
        <img 
          v-if="selectedCard === 'pay'" 
          src="../images/pay-orange.svg" 
          alt="analytic"
        >
        <img 
          v-else
          src="../images/pay.svg" 
          alt="analytic"
        >
        <p>Платежи</p>
      </div>
      <div 
        class="main__card"
        v-bind:class="{selected: selectedCard === 'settings'}"
        v-on:click="selectedCard = 'settings'"
      >
        <img 
          v-if="selectedCard === 'settings'" 
          src="../images/settings-orange.svg" 
          alt="analytic"
        >
        <img 
          v-else
          src="../images/settings.svg" 
          alt="analytic"
        >
        <p>Настройки</p>
      </div>
    </section>
  </article>
</template>

<script>
export default {
  name: "MainLeft",
  data: function () {
    return {
      selectedCard: 'users',
    }
  }
}
</script>

<style scoped>
  .main__left {
    display: flex;
    flex-direction: column;
    margin-bottom: 11px;
    margin-right: 104px;
  }

  .main__bread {
    display: flex;
    width: 236px;
    height: 59px;
    background-color: white;
    align-items: center;
    border-radius: 10px;
  }

  .main__bread select {
    background-color: white;
    border-radius: 10px;
    height: 100%;
    width: 177px;
    padding: 0 20px;
    font-style: normal;
    font-weight: bold;
    font-size: 15px;
    line-height: 130%;
    text-align: center;
    color: #2B2B2B;
    font-family: 'PT Sans', sans-serif;
  }

  .main__bread select:hover {
    cursor: pointer;
  }

  .main__bread img {
    margin-left: 16px;
  }

  .main__left-main {
    width: 177px;
    box-sizing: border-box;
    padding: 9px;
    background-color: white;
    margin-top: 11px;
    border-radius: 10px;
  }

  .main__card {
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 85px;
    width: 100%;
    font-family: 'PT Sans';
    padding: 19px 0 11px 0;
    font-style: normal;
    font-weight: bold;
    font-size: 15px;
    line-height: 130%;
    text-align: center;
    color: #000000;
    margin-bottom: 8px;
    border: 1px solid #E7ECF1;
    box-sizing: border-box;
    border-radius: 6px;
    transition: border 0.5s;
  }

  .main__card:hover {
    cursor: pointer;
    background-color: rgb(235, 250, 253);
    border: 1px solid rgb(235, 250, 253);
  }

  .selected {
    color: #FF7439;
    border: 1px solid #FF7439;
  }

  @media (max-width: 1200px) {
    .main__left {
      margin-right: 10px;
    }
  }
</style>