<template>
    <div class="search">
      <div class="type" @click.stop="showChose=true">
        {{currentName}}
        <img src="./img/down.png" v-if="!showChose" />
        <img src="./img/up.png" v-else />
        <!-- 下拉 菜单 -->
        <ul v-if="showChose" class="chose_muen">
          <li
            v-for="(v,k) in options"
            :key="k"
            @click.stop="choseStyle(v,k)"
            :class="{'active':value==index}"
          >{{v.text}}</li>
        </ul>
      </div>
</template>

<script>
//import 《组件名称》 from '《组件路径》';

export default {
     props:{
      options:{
        type:Array,
        default:[]
      },

    },
  data() {
 
    return {
       showChose:false,
       value:0,
       currentName:''
    };
  },
  //监听属性 类似于data概念
  computed: {},
  //监控data中的数据变化
  watch: {},
  //import引入的组件需要注入到对象中才能使用
  components: {

  },
  //生命周期 - 创建完成（可以访问当前this实例）
  created() {

  },
  //生命周期 - 挂载完成（可以访问DOM元素）
  mounted() {
    this.value=0;
  },
  //方法集合
  methods: {
     choseStyle(v,k){
       this.value=k;
       if(typeof v==String){
         this.currentName=v
       }else if(typeof v==Object){
         this.currentName=v.text
       }
     }
  },
  //生命周期 - 创建之前
  beforeCreate() {},
  //生命周期 - 挂载之前
  beforeMount() {},
  //生命周期 - 更新之前
  beforeUpdate() {},
  //生命周期 - 更新之后
  updated() {},
  //生命周期 - 销毁之前
  beforeDestroy() {},
  //生命周期 - 销毁完成
  destroyed() {},
  //如果页面有keep-alive缓存功能，这个函数会触发
  activated() {},
}
</script>
<style scoped lang="stylus">
 .search {
    width: 100%;
    height: 40px;
    padding: 0 15px;
    box-sizing: border-box;
    display: flex;
    align-items: center;
    justify-content: space-between;

    img {
      width: 0.3rem;
      height: 0.5rem;
    }

    .type {
      width: 24%;
      height: 30px;
      padding: 0 5px;
      margin-left: 0.4rem;
      background: #F5F5F5;
      position: relative;
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: 14px;
      box-sizing: border-box;

      img {
        width: 15px;
        height: 15px;
      }

      .chose_muen {
        position: absolute;
        bottom: -70px;
        left: 0;
        background: #fff;
        width: 100%;
        box-shadow: 0 4px 4px #ccc;

        li {
          line-height: 30px;
          text-align: center;
          font-size: 14px;
        }
      }
    }

    .search_input {
      width: 57%;
      background: #e5e5ee;

      input {
        width: 100%;
        height: 30px;
        padding-left: 10px;
        font-size: 13px;
      }
    }

    span {
      margin-left: 5px;
      font-size: 14px;
      color: #333;
      z-index: 99;
    }
  }

</style>