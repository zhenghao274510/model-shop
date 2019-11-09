<template>
  <view v-if="showBase" class="showSku" @click.stop="showBase=false">
    <!-- <div>选择规格</div> -->
    <view class="allskuinfo" @click.stop>
      <view class="title">
        <image :src="logo" alt class="oneimgs" />
        <view class="skuname">
          <text>{{SKname}}</text>
          <text>
            <text>￥{{currentSkuList.price}}</text>
          </text>
        </view>
        <image src="./img/cross.png" alt class="close" @click.stop="showBase=false" v-if="showCross" />
      </view>
      <view class="skudetail">
        <text
          @click.stop="changSku(index,item)"
          v-for="(item,index) in skuList"
          :key="index"
          :class="{'skuActive':active==index}"
        >{{item.val}}</text>
      </view>
      <view class="addnum">
        <view>
          <text style="font-size:13px;">数量</text>
          <text style="font-size:12px;">剩余{{currentSkuList.stock}}件</text>
        </view>
        <view class="buynum">
          <text @click.stop="del">-</text>
          <input type="number" v-model="val" />
          <text @click.stop="add">+</text>
        </view>
      </view>
      <view class="addbtn">
        <text class="first" @click.stop="onAdd">加入购物车</text>
        <text class="two" @click.stop="addBuy">立即下单</text>
      </view>
    </view>
  </view>
</template>

<script>
//import 《组件名称》 from '《组件路径》';

export default {
  props: {
    skuList: {
      type: [],
      default: []
    },
    SKname: {
      type: String,
      default: ""
    },
    logo: {
      type: String,
      default: ""
    },
    showCross:{
      type:Boolean,
      default:false
    }
  },
  data() {
    return {
      active: 0,
      currentSkuList: [],
      val: 1
    };
  },
  //监听属性 类似于data概念
  computed: {},
  //监控data中的数据变化
  watch: {},
  //import引入的组件需要注入到对象中才能使用
  components: {},
  //生命周期 - 创建完成（可以访问当前this实例）
  created() {},
  //生命周期 - 挂载完成（可以访问DOM元素）
  mounted() {
    this.currentSkuList = this.skuList[0];
  },
  //方法集合
  methods: {
    changSku(index, item) {
      this.active = index;
      this.currentSkuList = this.skuList[index];
      this.val=1;
    },
    onAdd() {
      this.$emit("addCar");
    },
    onBuy() {
      this.$emit("addBuy");
    },
    del() {
      if (this.val > 1) {
        this.val -= 1;
      }
    },
    add() {
      if (this.val <this.currentSkuList.stock) {
        this.val += 1;
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
  activated() {}
};
</script>
<style scoped lang="stylus">
.showSku {
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 99;
  background: rgba(0, 0, 0, 0.45);

  .allskuinfo {
    background: #fff;
    width: 100%;
    position: fixed;
    bottom: 0;
    left: 0;

    .title {
      padding: 0.2rem;
      position: relative;
      display: flex;
      align-items: center;
      justify-content: center;

      .oneimgs {
        position: absolute;
        top: -20px;
        left: 20px;
        width: 100px;
        height: 100px;
        border-radius: 5px;
      }

      .skuname {
        p {
          font-size: 14px;
          display: flex;

          span {
            color: #FE552E;
          }
        }
      }

      .close {
        position: absolute;
        right: 20px;
        top: 20px;
        width: 22px;
        height: 22px;
      }
    }
  }

  .skudetail {
    display: flex;
    padding: 20px;
    margin-top: 40px;
    flex-wrap: wrap;

    span {
      padding: 7px 15px;
      border: 1px solid #c1c1c1;
      font-size: 12px;
      margin-right: 10px;
      margin-bottom: 10px;
      border-radius: 15px;
    }

    .skuActive {
      background: #72D241;
      color: #fff;
      border: none;
    }
  }

  .addnum {
    display: flex;
    padding: 10px 20px;
    align-items: center;
    justify-content: space-between;

    .buynum {
      display: flex;
      align-items: center;

      span {
        width: 25px;
        height: 28px;
        // border: 1px solid #ccc;
        border-radius: 2rpx;
        line-height: 30px;
        text-align: center;
        font-size: 12px;
      }

      input {
        margin: 0 5px;
        width: 35px;
        height: 20px;
        line-height: 20px;
        font-size: 12px;
        text-align: center;
        background: #F6F6F6;
        color: #1A1A1A;
        // border: 1px solid #ccc;
      }
    }
  }
}
</style>