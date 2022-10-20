<template>
  <checkBox :options="options" :columns="columns"/>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import checkBox from './components/checkBox.vue';

export default defineComponent({
  name: 'App',
  components: {
    checkBox
  },
  data(){
    return{
        columns:3,
        options:[
        {
            value:1,
            label: "a2342342343243244234234324324",
        },
        {
            value:2,
            label: "b",
        },
        {
            value:3,
            label: "c",
        },
        {
            value:4,
            label: "d32432442342343",
        },
        {
            value:5,
            label: "e",
        },
        {
            value:6,
            label: "f",
        },]
    }
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
