<template>
  <div id="app">
    <el-row>
      <el-col :span="7"
              class="order-list list-left">

        <!-- S 商品订单模块 -->
        <el-tabs>
          <el-tab-pane>
            <span slot="label"
                  class="tabs">点餐</span>
            <el-scrollbar>
              <el-table :data="tableData"
                        border
                        show-summary
                        :summary-method="totalArr"
                        style="width:100%">
                <el-table-column label="商品"
                                 prop="goodsName">
                </el-table-column>
                <el-table-column label="数量"
                                 prop="count"
                                 width="50">
                </el-table-column>
                <el-table-column label="金额"
                                 prop="price"
                                 width="70">
                  <template slot-scope="scop">
                    <span>{{ scop.row.price * scop.row.count }}</span>
                  </template>
                </el-table-column>
                <el-table-column label="操作"
                                 fixed="right"
                                 width="100">
                  <template slot-scope="scope">
                    <el-button @click="addCount(scope.row)"
                               type="text"
                               size="small">增加</el-button>
                    <el-button @click="delSingle(scope.row)"
                               type="text"
                               size="small">删除</el-button>
                  </template>
                </el-table-column>
              </el-table>
            </el-scrollbar>
          </el-tab-pane>
          <el-tab-pane>
            <span slot="label"
                  class="tabs">挂单</span>
          </el-tab-pane>
          <el-tab-pane>
            <span slot="label"
                  class="tabs">外卖</span>
          </el-tab-pane>
        </el-tabs>
        <!-- E 商品订单模块 -->

        <!-- S 操作模块 -->
        <div class="order-btn">

          <el-button type="success">挂单</el-button>
          <el-button type="danger"
                     @click="delAll">删除</el-button>
          <el-button type="warning"
                     @click="checkout">结账</el-button>

        </div>
        <!-- E 操作模块 -->

      </el-col>
      <el-col :span="17"
              class="order-list list-right">

        <!-- S 常用商品模块 -->
        <div class="often">
          <div class="often__top">
            <span class="often__top-title">常用商品</span>
          </div>
          <ul class="often__list clear-fix">
            <li v-for="item in oftenGoods"
                :key="item.goodsId"
                class="often__list__item"
                @click="addOrderList(item)">
              <span class="often__list__item-title">{{ item.goodsName }}</span>
              <span class="often__list__item-pice">¥{{ item.price }}</span>
            </li>
          </ul>
        </div>
        <!-- E 常用商品模块 -->

        <!-- S 商品类型模块 -->
        <div class="types">
          <el-tabs>

            <el-tab-pane label="汉堡">
              <ul class="cookie">
                <li class="cookie__item"
                    v-for="item in type0Goods"
                    :key="item.goodsId"
                    @click="addOrderList(item)">
                  <img class="cookie__item-pic"
                       :src="item.goodsImg"
                       :alt="item.goodsName">
                  <span class="cookie__item-name">{{ item.goodsName }}</span>
                  <span class="cookie__item-price">¥{{ item.price }}</span>
                </li>
              </ul>
            </el-tab-pane>
            <!-- /汉堡模块 -->

            <el-tab-pane label="小食">
              <ul class="cookie">
                <li class="cookie__item"
                    v-for="item in type1Goods"
                    :key="item.goodsId"
                    @click="addOrderList(item)">
                  <img class="cookie__item-pic"
                       :src="item.goodsImg"
                       :alt="item.goodsName">
                  <span class="cookie__item-name">{{ item.goodsName }}</span>
                  <span class="cookie__item-price">¥{{ item.price }}</span>
                </li>
              </ul>
            </el-tab-pane>
            <!-- /小食模块 -->

            <el-tab-pane label="饮料">
              <ul class="cookie">
                <li class="cookie__item"
                    v-for="item in type2Goods"
                    :key="item.goodsId"
                    @click="addOrderList(item)">
                  <img class="cookie__item-pic"
                       :src="item.goodsImg"
                       :alt="item.goodsName">
                  <span class="cookie__item-name">{{ item.goodsName }}</span>
                  <span class="cookie__item-price">¥{{ item.price }}</span>
                </li>
              </ul>
            </el-tab-pane>
            <!-- /饮料模块 -->

            <el-tab-pane label="套餐">
              <ul class="cookie">
                <li class="cookie__item"
                    v-for="item in type3Goods"
                    :key="item.goodsId"
                    @click="addOrderList(item)">
                  <img class="cookie__item-pic"
                       :src="item.goodsImg"
                       :alt="item.goodsName">
                  <span class="cookie__item-name">{{ item.goodsName }}</span>
                  <span class="cookie__item-price">¥{{ item.price }}</span>
                </li>
              </ul>
            </el-tab-pane>
            <!-- 套餐模块 -->

          </el-tabs>
        </div>
        <!-- E 商品类型模块 -->

      </el-col>
    </el-row>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      msg: 'amazePos',
      totalCount: 0,
      totalMoney: 0,
      tableData: [],
      oftenGoods: null,
      type0Goods: null,
      type1Goods: null,
      type2Goods: null,
      type3Goods: null
    }
  },
  created () {
    axios.get('http://jspang.com/DemoApi/oftenGoods.php')
      .then(response => {
        console.log(response)
        this.oftenGoods = response.data
      })
      .catch(error => {
        console.log(error)
        alert('网络错误不可访问')
      })
    axios.get('http://jspang.com/DemoApi/typeGoods.php')
      .then(response => {
        console.log(response)
        this.type0Goods = response.data[0]
        this.type1Goods = response.data[1]
        this.type2Goods = response.data[2]
        this.type3Goods = response.data[3]
      })
      .catch(error => {
        console.log(error)
        alert('网络错误不可访问')
      })
  },
  mounted () {
    const orderHeight = document.body.clientHeight
    for (let i = 0; i < 2; i++) {
      document.getElementsByClassName('order-list')[i].style.height = orderHeight + 'px'
    }
  },
  methods: {
    /**
     * @param goods     object[必选]         商品对象
     */
    addOrderList (goods) {
      let isHave = false
      for (let i = 0; i < this.tableData.length; i++) {
        if (this.tableData[i].goodsId === goods.goodsId) {
          isHave = true
        }
      }
      if (isHave) {
        // 使用过滤器选取去和当前商品id对应的数组
        let arr = this.tableData.filter(o => o.goodsId === goods.goodsId)
        arr[0].count++
      } else {
        let newItem = { goodsId: goods.goodsId, goodsName: goods.goodsName, price: goods.price, count: 1 }
        this.tableData.push(newItem)
      }
      this.setAllCount()
    },
    totalArr () {
      return ['合计', this.totalCount, this.totalMoney]
    },
    setAllCount () {
      this.totalCount = 0
      this.totalMoney = 0
      this.tableData.forEach(element => {
        this.totalCount = this.totalCount + element.count
        this.totalMoney = this.totalMoney + (element.price * element.count)
      })
    },
    addCount (goods) {
      goods.count++
      this.setAllCount()
    },
    delSingle (goods) {
      let arr = this.tableData.filter(o => o.goodsId !== goods.goodsId)
      this.tableData = arr
      this.setAllCount()
    },
    delAll () {
      this.tableData = []
      this.totalCount = 0
      this.totalMoney = 0
    },
    checkout () {
      if (this.totalCount !== 0) {
        this.tableData = []
        this.totalCount = 0
        this.totalMoney = 0
        this.$message('结账成功，感谢你又为店里出了一份力')
      } else {
        this.$message('不能空结，老板了解你急切的心情')
      }
    }

  }
}
</script>
<style lang="less" scoped>
/* 点餐选项warp */
.order-btn {
  padding-top: 20px;
  text-align: center;
}

/* 点餐warp */
.list-right {
  background: #f5f7fa;
}

/* 商品warp */
.list-left {
  border-right: 1px solid rgb(222, 225, 233);
}

/* 自定义tab选项卡 */
.tabs {
  padding: 20px;
}

/* 常用商品模块
-------------------------------------------------------------- */
.often {
  background: #fff;
}
.often__top {
  padding: 8.5px 10px;
  border-bottom: 1px solid #e4e7ed;
  background: #f5f7fa;
}
.often__top-title {
  font-size: 14px;
}
.often__list {
  list-style: none;
  padding: 15px 40px;
}
.often__list__item {
  float: left;
  padding: 10px;
  margin: 5px 5px;
  border: 1px solid #e4e7ed;
  font-size: 14px;
  border-radius: 3px;
}
.often__list__item:hover {
  background-color: #409eff;
  color: #fff;
  .often__list__item-pice {
    color: deeppink;
  }
}
.often__list__item-pice {
  color: #409eff;
  font-weight: bold;
}

/* 商品列表模块
-------------------------------------------------------------- */
.types {
  padding-left: 20px;
}

/* tab部分 */
.cookie__item {
  float: left;
  width: 25%;
  border: 1px solid #e5e9f2;
  height: auto;
  overflow: hidden;
  background-color: #fff;
  padding: 2px;
  margin: 2px;
}
.cookie__item-pic {
  float: left;
  width: 40%;
}
.cookie__item-name {
  display: block;
  padding: 5px 10px;
  overflow: hidden;
}
.cookie__item-price {
  display: block;
  padding-left: 13px;
  overflow: hidden;
  color: deeppink;
  font-weight: bold;
}
</style>
