<template>
  <div>
    <el-select :value="bindValue" @change="change" v-el-loadmore:number="loadMore(number)">
      <el-input size="small" v-model="search"></el-input>
      <el-option style="width: 200px" v-for="(item, i) in comOption" :key="i" :value="item.value" :label="item.label">
      </el-option>
    </el-select>
  </div>
</template>
<script>
  import Vue from "vue";
  // 自定义一个vue指令监听滚动条
  Vue.directive(
    'el-loadmore', {
      bind(el, binding) {
        // 获取element-ui定义好的scroll盒子
        const SELECT_DOM = el.querySelector('.el-select-dropdown .el-scrollbar .el-select-dropdown__wrap');
        // 打印一下看看有没有获取到 element-ui 定义的scroll盒子
        console.log('SELECT_DOM', SELECT_DOM)
        SELECT_DOM.addEventListener('scroll', function () {
          /**
           * scrollHeight 获取元素内容高度(只读)
           * scrollTop 获取设置元素的偏移值,常用于计算滚动条的位置, 当一个元素的容器没有产生垂直方向的滚动条时, scrollTop的值默认为0.
           * clientHeight 读取元素的可见高度(只读)
           * 如果元素滚动到底, 下面等式返回true, 没有则返回false:
           * ele.scrollHeight - ele.scrollTop === ele.clientHeight;
           */
          const condition = this.scrollHeight - this.scrollTop <= this.clientHeight;
          // 判断 condition 的值是否为true，为true 时调用 loadMore方法
          if (condition) binding.value();
        });
      }
    }
  )

  export default {
    data() {
      return {
        number: 10,
        copyOption: [],
        option: [],
        watchValue: '',
        search: ''
      }
    },
    model: {
      prop: 'bindValue',
      event: 'change'
    },
    props: {
      bindValue: String,
      options: Array
    },
    created() {
      this.option = JSON.parse(JSON.stringify(this.options))
      this.copyOption = JSON.parse(JSON.stringify(this.options));
    },
    computed: {
      comOption() {
        if (this.option.length > 10) {
          return this.option.slice(0, this.number)
        } else {
          return this.option
        }
      },
    },
    methods: {
      change(val) {
        this.$emit('change', val);
        // this.$emit('eleChange',)
      },
      loadMore(n) {
        return () => this.number += 5 //每次滚动到底部可以新增条数  可自定义
      },
    },
    watch: {
      search(newValue, oldValue) {
        if (newValue) {
          this.option = this.copyOption.filter(item => {
            return item.value.indexOf(newValue) > -1
          })
        } else {
          this.option = this.copyOption;
        }

      }
    }
  }

</script>
<style>
  /* .el-select-dropdown__empty {
    visibility: hidden;
  } */
  .el-select-dropdown {
    max-width: 40%;
  }

  .el-select-dropdown__item {
    overflow: visible;
  }

</style>
