<template>
  <Title title="Catatan Pengeluaran"/>
  <FormPengeluaran @entri-pengeluaran="entriPengeluaran($event)"/>
  <h2>Total Pengeluaran : {{ totalPengeluaran }}</h2>
  <h2 v-if="warning" class="warning">Pengeluaran Anda Terlalu Banyak !!! </h2>
  <ListPengeluaran v-if="showList" :dataPengeluaran="dataPengeluaran"/>
</template>

<script>

import Title from './components/Title.vue';
import ListPengeluaran from './components/ListPengeluaran.vue';
import FormPengeluaran from './components/FormPengeluaran.vue';

export default {
  name: 'App',
  components: {
    Title,ListPengeluaran,FormPengeluaran
  },
  data(){
    return{
      dataPengeluaran : [
        // { nominal: '20000', keterangan: "makan siang"},
        // { nominal: '25000', keterangan: "pulsa"},
        // { nominal: '50000', keterangan: "listrik"},
        ],
        warning:false
    }
  },
  methods:{
    entriPengeluaran(event){
      this.dataPengeluaran.push(event);
    }
  },
  computed:{
    showList: function(){
      return this.dataPengeluaran.length>0;
    },
    totalPengeluaran: function(){
      return this.dataPengeluaran.reduce((accum, item) => accum+parseInt(item.nominal),0);
    },
  },
  watch:{
    totalPengeluaran:function(val)
    {
      if(val > 100000)
      {
        this.warning = true;
      }
    }
  },
}
</script>

<style>
#app{
  font-family: Avenir, Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
h2{
  text-align: center;
}
.warning{
  color: red;
}
</style>