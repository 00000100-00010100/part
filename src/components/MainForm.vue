<template>
<main>
<article>
<form>
  <div class="main-form">
    <p>
      This is a tool for auto-generating markdown for reporting entries for 
      <a href="https://github.com/2020PB/police-brutality" target="_blank" rel="noopener">2020 Police Brutality</a>.
    </p>

    <h4>Title</h4>
    <textarea type="text" v-model="title"></textarea>

    <h4>Date</h4>
    <date-picker v-model="date" type="date"></date-picker>

    <h4>Description</h4>
    <textarea rows="4" id="description" v-model="description"></textarea>

    <h4>Links</h4>
    <textarea v-model="link1"></textarea>
    <textarea v-model="link2"></textarea>
    <textarea v-model="link3"></textarea>

    <!--<h4>Tags</h4>
    <select v-model="tagMultiSelect" multiple>
      <option>Police Brutality</option>
      <option>Free Press Violation</option>
      <option>Free Speech Violation</option>
      <option>Destruction of Property</option>
    </select>
    <br>
    <button v-on:click="copyToClipboard">Copy</button>-->
    <pre id="generated-markdown">{{'### ' + title + " | " + ( (date !== null) ? date.toDateString() : '' ) + '\n\n' +
      description + '\n\nid: ' + generateId() + '\n\n' +
      '**Links**\n\n' +
      ( (link1 !== '') ? ('* ' + link1 + '\n') : '' ) +
      ( (link2 !== '') ? ('* ' + link2 + '\n') : '' ) +
      ( (link3 !== '') ? ('* ' + link3 + '\n') : '' ) + '\n'
      }}</pre>
  
  </div>
  </form>
  </article>
  </main>
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
  },
  methods: {
    // todo: this doesnt copy the formatting and refreshes the page clearing the form :(
    copyToClipboard: function () {
      var aux = document.createElement("div");
      aux.setAttribute("contentEditable", 'true');
      var generatedMarkdown = document.getElementById('generated-markdown');
      if(generatedMarkdown !== null) {
        aux.innerHTML = generatedMarkdown.innerHTML;
      }
      aux.setAttribute("onfocus", "document.execCommand('selectAll',false,null)"); 
      document.body.appendChild(aux);
      aux.focus();
      document.execCommand("copy");
      document.body.removeChild(aux);
    },
    generateId: function() {
      return '' + Math.random().toString(36).substr(2, 12);
    }
  }
})
export default class MainForm extends Vue {
  @Prop() private msg!: string;
}

</script>

<style scoped>
  pre {
    white-space: pre-wrap;       /* Since CSS 2.1 */
    white-space: -moz-pre-wrap;  /* Mozilla, since 1999 */
    white-space: -pre-wrap;      /* Opera 4-6 */
    white-space: -o-pre-wrap;    /* Opera 7 */
    word-wrap: break-word;       /* Internet Explorer 5.5+ */
  }
  .description {

  }
</style>
