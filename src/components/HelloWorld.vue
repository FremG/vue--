<template>
  <div>
    <!-- <base-checkbox v-model="flag"></base-checkbox> -->
    <ele-select v-model="flag" :options="options"></ele-select>
    <!-- <el-select v-model="flag" filterable :filter-method="filterMethods" @focus="focusFn">
      <el-option v-for="(item, i) in options" :key="i" :value="item.value" :label="item.label" >

      


      </el-option>
    </el-select> -->


    <!-- <el-table :data="tableData">
       <el-table-column min-width="130" :prop="item.label" :label="item.label" align="center" v-for="(item, i) in options" :key="i">
          <template slot-scope="scope">
            <span>{{scope.row.mm}}</span>
            <el-input size="mini" style="min-width: 100px" v-model="scope.row.mm" type="number"></el-input>
          </template>
        </el-table-column>
    </el-table> -->
  </div>
</template>
<script>
import eleSelect from './ele-select';
import Vue from 'vue'

// Vue.component('base-checkbox', {
//   model: {
//     prop: 'checked',
//     event: 'change'
//   },
//   props: {
//     checked: Boolean
//   },
//   template: `
//     <input
//       type="checkbox"
//       v-bind:checked="checked"
//       v-on:change="$emit('change', $event.target.checked)"
//     >
//   `
// })
  export default {
    components: {
      eleSelect
    },
    data() {
      return {
        tableData: [{mm:123}],
        mm:123,
        flag: null,
        value: 123,
        options: [],
        copyOption: []
      }
    },
    methods: {
      onFocus() {
        console.log(this.value)
      },
      filterMethods(val) {  
            this.flag = val;
          if (val) { 
            this.options = this.copyOption.filter( item => {
              return String(item.value).indexOf(val) > -1
            });
          
          } else {
            this.options = JSON.parse(JSON.stringify(this.copyOption))
          }
      },
      focusFn() {
        this.filterMethods(this.flag);
      }
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
          value: String(i),
          label: String(i)
        });
        this.tableData.push({
          mm:i
        })
      }
      this.copyOption = JSON.parse(JSON.stringify(this.options));
    },
    watch: {
      flag(a) {
        console.log(a)
      }
    }
  }
</script>