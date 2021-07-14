<template>

  <div id="app">

    <app-header></app-header>
    <contacts></contacts>

  </div>

</template>

<script>
import AppHeader from './components/AppHeader.vue';
import Contacts from './components/Contacts.vue';

export default {
  data() {
    return {

    };
  },
  components: {
    Contacts,
    AppHeader,
  },
};

</script>
<style lang="scss">
body {
  background-color: gray;
}

</style>
