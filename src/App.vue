<template>
  <div id="app">
    <MainForm msg="Welcome to Your Vue.js + TypeScript App" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import MainForm from './components/MainForm.vue';

@Component({
  components: {
    MainForm,
  },
})

export default class App extends Vue {}
</script>
