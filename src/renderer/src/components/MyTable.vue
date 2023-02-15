<script setup lang="ts">
import { ref } from 'vue';

let hover = ref(false);

const data = ref([
  {
    id: '1',
    company: 'foo',
    contact: 'bla',
    country: 'bing',
    isHovered: false
  },
  {
    id: '2',
    company: 'bar',
    contact: 'shma',
    country: 'hiff',
    isHovered: false
  }
]);

const films = [
  "A Throne Too Far",
  "The Cat Wasn't Invited",
  "You Only Meow Once",
  "Catless in Seattle"
];

function createRow(){
  data.value.push({
    id: '3',
    company: 'yo',
    contact: 'ji',
    country: 'gong',
    isHovered: false
  });
}

function showData(){
  alert(JSON.stringify(data));
}

function mouseOver(index: number){
  data.value.splice(index, 1, {...data.value[index], isHovered: true});
}
function mouseLeave(index: number){
  data.value.splice(index, 1, {...data.value[index], isHovered: false});
}
</script>

<template>
  <table>
    <thead>
      <tr>
        <th>Company</th>
        <th>Contact</th>
        <th>Country</th>
      </tr>
    </thead>

    <tbody>
      <tr v-for="(row, index) in data" :key="row.id">
        <td>
          <input v-model="row.company">
        </td>
        <td>
          <input list="films" v-model="row.contact">
        </td>
        <td>{{row.country}}</td>
      </tr>
    </tbody>
  </table>

  <datalist id="films">
    <option v-for="film in films">{{film}}</option>
  </datalist>


  <button @click="createRow">Add Row</button>
  <button @click="showData">Show Data</button>


</template>

<style lang="less">
@import 'simpledotcss';

.uneditable-table-cell {
  visibility: visible;
}

.uneditable-table-cell:hover {
  visibility: hidden;
}

.editable-table-cell {
  visibility: hidden;
}

.editable-table-cell:hover {
  visibility: visible;
}
</style>
