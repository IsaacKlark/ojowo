<template>
<main class="main">
  <MainLeft />
  <section class="main__right">
    <MainRightHead />
    <MainRightTable />
  </section>
</main>
</template>
<script>
import MainLeft from './MainLeft';
import MainRightHead from './MainRIghtHead';
import MainRightTable from './MainRightTable';

export default {
  name: "Main",
  components: {
    MainLeft,
    MainRightHead,
    MainRightTable,
  }
};
</script>

<style scoped>
  .main {
    display: flex;
  }

  .main__right {
    max-width: 1269px;
    box-sizing: border-box;
  }
</style>