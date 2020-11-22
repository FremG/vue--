<template>
  <div>
    <ele-select v-model="flag" :options="options" @change="() => {change('123456789')}"></ele-select>
  </div>
</template>
<script>
import eleSelect from './ele-select';
import Vue from 'vue'

  export default {
    components: {
      eleSelect
    },
    data() {
      return {
        flag: null,
        options: [],
      }
    },
    methods: {
      change(a) {
        console.log(a)
      },
    },
    created() {
      
         class a {
                constructor(mm) {
                      console.log(mm)
                }
            }
            let A = new a('mm');

      for (var i =0; i< 10000;i++) {
        this.options.push({
          value: String(i) +'mmmmmmmmmmmmmmmmmmffffffffffffffffffffffmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmm',
          label: String(i) + 'mmmmmmmmmmmmmffffffffffffffffffffffffffmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmm'
        });
      }
    },
    watch: {
      flag(a) {
        console.log(a)
      }
    }
  }
</script>