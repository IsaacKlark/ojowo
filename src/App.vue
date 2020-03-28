<template>
  <div id="app" v-on:click="e => hideCalendarZone(e)">
    <Header />
    <Main />
  </div>
</template>

<script>
import Header from './components/Header';
import Main from './components/Main';
export default {
  name: 'App',
  components: {
    Header,
    Main,
  },
  methods: {
    hideCalendarZone: function (e) {
      if (!e.target.className.includes('calendar-child')) {
        document.querySelector('.calendar-zone').style.display = "none";
      }
    }
  }
}
</script>

<style>
body {
  background-color: #F0F6FC;
  padding: 0 38px;
  margin: 0;
  font-family: 'Montserrat', sans-serif;
}

button, select, input {
  border: 0;
  outline: 0;
}
</style>
