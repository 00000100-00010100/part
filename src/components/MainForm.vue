<template>
  <div class="main-form">
    <p>
      This is a tool for auto-generating markdown for reporting entries for 
      <a href="https://github.com/2020PB/police-brutality" target="_blank" rel="noopener">2020 Police Brutality</a>.
    </p>
    <h3>Title</h3>
    <ul>
      <li>
        <input type="text" v-model="title">
      </li>
    </ul>
    <h3>Date</h3>
    <ul>
      <li>
        <div>
          <date-picker v-model="date" type="date"></date-picker>
        </div>
      </li>
    </ul>
    <h3>Description</h3>
    <ul>
      <li>
        <textarea v-model="description"></textarea>
      </li>
    </ul>
    <h3>Links</h3>
    <ul>
      <li>
        <input v-model="link1">
      </li>
      <li>
        <input v-model="link2">
      </li>
      <li>
        <input v-model="link3">
      </li>
    </ul>
    <h3>Tags</h3>
    <ul>
      <li>
        <select v-model="tagMultiSelect" multiple>
          <option>Police Brutality</option>
          <option>Free Press Violation</option>
          <option>Free Speech Violation</option>
          <option>Destruction of Property</option>
        </select>
      </li>
    </ul>
    <pre>{{'### ' + title + " | " + ( (date !== null) ? date.toDateString() : '' ) + '\n\n' +
      description + '\n\n' +
      '**Links**\n\n' +
      ( (link1 !== '') ? ('* ' + link1 + '\n') : '' ) +
      ( (link2 !== '') ? ('* ' + link2 + '\n') : '' ) +
      ( (link3 !== '') ? ('* ' + link3 + '\n') : '' )
      }}

      {{tagMultiSelect}}
    </pre>
  
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import DatePicker from "vue2-datepicker";
import 'vue2-datepicker/index.css';

@Component({
  components: {
    DatePicker,
  },
  data: function() {
    return{
      title:'',
      description:'',
      date: null,
      link1:'',
      link2:'',
      link3:'',
      tagMultiSelect:[],
    }
  }
})
export default class MainForm extends Vue {
  @Prop() private msg!: string;
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
