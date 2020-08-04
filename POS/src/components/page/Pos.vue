<template>
  <div class="pos">
     <el-row>
       <el-col :span='7' class="pos-order" id="order-list">
         <el-tabs>
           <el-tab-pane label="点餐">
              <el-table :data="tableData" border width="100%">
                <el-table-column prop="goodsName" label="商品名称"></el-table-column>
                <el-table-column prop="count" label="数量" width="50"></el-table-column>
                <el-table-column prop="price" label="金额" width="70"></el-table-column>
                <el-table-column label="操作" width="100" fixed="right">
                   <template slot-scope="scope">
                      <el-button type="text" size="small" @click="delSingleGoods(scope.row)">删除</el-button>
                      <el-button type="text" size="small" @click="addOrderList(scope.row)">添加</el-button>
                   </template>
                </el-table-column>
              </el-table>
              <div class="totalDiv">
                  <small>数量：</small>{{totalCount}}  &nbsp;&nbsp;&nbsp;&nbsp;   <small>金额：</small>{{totalMoney}}元
              </div>
              <div class="div-btn">
                <el-button type="warning">挂单</el-button>
                <el-button type="danger" @click="delAllGoods()">删除</el-button>
                <el-button type="success" @click="checkout()">结账</el-button>
              </div>
           </el-tab-pane>
           <el-tab-pane label="挂单">
              挂单
           </el-tab-pane>
           <el-tab-pane label="外卖">
              外卖
           </el-tab-pane>
         </el-tabs>
       </el-col>
       <el-col :span="17">
         <div class="often-goods">
           <div class="title">常用商品</div>
           <div class="often-goods-list">
             <ul>
               <li v-for="goods in oftenGoods" :key="index" @click="addOrderList(goods)">
                 <span>{{goods.goodsName}}</span>
                 <span class="o-price">¥{{goods.price}}元</span>
               </li>
             </ul>
           </div>
         </div>
         
         <div class="good-type">
            <el-tabs>
              <el-tab-pane label="汉堡">
                  <div>
                    <ul class='cookList'>
                      <li v-for="goods in type0Goods" @click="addOrderList(goods)">
                        <span class="foodImg"><img src="https://dss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=592949798,3796715208&fm=26&gp=0.jpg" width="100%"></span>
                        <span class="foodName">{{goods.goodsName}}</span>
                        <span class="foodPrice">￥{{goods.price}}元</span>
                      </li>
                    </ul>
                  </div>
              </el-tab-pane>
              <el-tab-pane label="小食">
                  <div>
                    <ul class='cookList'>
                      <li v-for="goods in type1Goods" @click="addOrderList(goods)">
                        <span class="foodImg"><img src="https://dss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=592949798,3796715208&fm=26&gp=0.jpg" width="100%"></span>
                        <span class="foodName">{{goods.goodsName}}</span>
                        <span class="foodPrice">￥{{goods.price}}元</span>
                      </li>
                    </ul>
                  </div>
              </el-tab-pane>
              <el-tab-pane label="饮料">
                  <div>
                    <ul class='cookList'>
                      <li v-for="goods in type2Goods" @click="addOrderList(goods)">
                        <span class="foodImg"><img src="https://dss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=592949798,3796715208&fm=26&gp=0.jpg" width="100%"></span>
                        <span class="foodName">{{goods.goodsName}}</span>
                        <span class="foodPrice">￥{{goods.price}}元</span>
                      </li>
                    </ul>
                  </div>
              </el-tab-pane>
              <el-tab-pane label="套餐">
                  <div>
                    <ul class='cookList'>
                      <li v-for="goods in type3Goods" @click="addOrderList(goods)">
                        <span class="foodImg"><img src="https://dss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=592949798,3796715208&fm=26&gp=0.jpg" width="100%"></span>
                        <span class="foodName">{{goods.goodsName}}</span>
                        <span class="foodPrice">￥{{goods.price}}元</span>
                      </li>
                    </ul>
                  </div>
              </el-tab-pane>
            </el-tabs>
         </div>
       </el-col>
     </el-row>
  </div>
</template>

<script>
export default {
  name: 'pos',
  data(){
    return{
      totalCount:0,
      totalMoney:0,
      tableData:[
        /* {
           goodsName:'可口可乐',
           count:1,
           price:8
         },
         {
           goodsName:'香辣鸡腿堡',
           count:1,
           price:18
         },
         {
           goodsName:'爱心薯条',
           count:1,
           price:12
         },
         {
           goodsName:'甜筒',
           count:1,
           price:5
         }*/
      ],
      oftenGoods:[
        {
              goodsId:1,
              goodsName:'香辣鸡腿堡',
              price:18
          }, {
              goodsId:2,
              goodsName:'田园鸡腿堡',
              price:15
          }, {
              goodsId:3,
              goodsName:'和风汉堡',
              price:15
          }, {
              goodsId:4,
              goodsName:'快乐全家桶',
              price:80
          }, {
              goodsId:5,
              goodsName:'脆皮炸鸡腿',
              price:10
          }, {
              goodsId:6,
              goodsName:'魔法鸡块',
              price:20
          }, {
              goodsId:7,
              goodsName:'可乐大杯',
              price:10
          }, {
              goodsId:8,
              goodsName:'雪顶咖啡',
              price:18
          }, {
              goodsId:9,
              goodsName:'大块鸡米花',
              price:15
          }, {
              goodsId:10,
              goodsName:'香脆鸡柳',
              price:17
          },
          {
              goodsId:11,
              goodsName:'小份薯条',
              price:6
          },
          {
              goodsId:12,
              goodsName:'大份薯条',
              price:10
          }
      ],
      type0Goods:[
          {
              goodsId:1,
              goodsImg:"https://dss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=592949798,3796715208&fm=26&gp=0.jpg",
              goodsName:'香辣鸡腿堡',
              price:18
          }, {
              goodsId:2,
              goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
              goodsName:'田园鸡腿堡',
              price:15
          }, {
              goodsId:3,
              goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
              goodsName:'和风汉堡',
              price:15
          }
      ],
      type1Goods:[
         {
              goodsId:5,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
              goodsName:'脆皮炸鸡腿',
              price:10
          }, {
              goodsId:6,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
              goodsName:'魔法鸡块',
              price:20
          },
           {
              goodsId:9,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
              goodsName:'大块鸡米花',
              price:15
          }, {
              goodsId:20,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
              goodsName:'香脆鸡柳',
              price:17
          }
      ],
       type2Goods:[
         {
              goodsId:7,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
              goodsName:'可乐大杯',
              price:10
          }, {
              goodsId:8,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
              goodsName:'雪顶咖啡',
              price:18
          }
       ],
        type3Goods:[
          {
              goodsId:4,
               goodsImg:"http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
              goodsName:'快乐全家桶',
              price:80
          }
        ]
    }
  },
  mounted:function(){
    var orderHeight=document.body.clientHeight;
    document.getElementById('order-list').style.height=orderHeight+'px';
  },
  methods:{
    addOrderList(goods){
            this.totalCount=0; //汇总数量清0
            this.totalMoney=0;
            let isHave=false;
            //判断是否这个商品已经存在于订单列表
            for (let i=0; i<this.tableData.length;i++){
                console.log(this.tableData[i].goodsId);
                if(this.tableData[i].goodsId==goods.goodsId){
                    isHave=true; //存在
                }
            }
            //根据isHave的值判断订单列表中是否已经有此商品
            if(isHave){
                //存在就进行数量添加
                 let arr = this.tableData.filter(o =>o.goodsId == goods.goodsId);
                 arr[0].count++;
                 //console.log(arr);
            }else{
                //不存在就推入数组
                let newGoods={goodsId:goods.goodsId,goodsName:goods.goodsName,price:goods.price,count:1};
                 this.tableData.push(newGoods);

            }

            
             this.getAllMoney();

      },
      //删除单个商品
      delSingleGoods(goods){
        this.tableData=this.tableData.filter(o =>o.goodsId !=goods.goodsId);
        this.getAllMoney();
      },
      //删除所有商品
      delAllGoods(){
        this.tableData=[];
        this.totalCount=0;
        this.totalMoney=0;
      },
      //模拟结账
      checkout(){
        if(this.totalCount!=0){
          this.tableData=[];
          this.totalCount=0;
          this.totalMoney=0;
          this.$message({
            message:'结账成功，祝您用餐愉快！！！',
            type:'success'
          });
        }else{
          this.$message.error('不能空结');
        }
      },
      //汇总总数量和金额
      getAllMoney(){
        this.totalCount=0;
        this.totalMoney=0;
        //进行数量和价格的汇总计算
        if(this.tableData){
          this.tableData.forEach((element) => {
                this.totalCount+=element.count;
                this.totalMoney=this.totalMoney+(element.price*element.count);   
            }
            );
        }
      }

  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .pos-order{
    background-color: #F9FAFC;
    border-left: 1px solid #C0ccDA;
  }
  .div-btn{
    margin-top: 10px;
  }
  .title{
    height: 20px;
    border-bottom: 1px solid #d3dce6;
    background-color: #F9FAFC;
    padding: 10px;
    text-align: left;
  }
  .often-goods-list ul li{
    list-style: none;
    float: left;
    padding: 10px;
    margin: 10px;
    border: 1px solid #e5e7f2;
    background-color: #FFF;
  }
  .o-price{
    color: #58B7FF;
  }
  .good-type{
    clear: both;
    margin-left: 10px;
    border-top: 1px solid #d3dce6;
  }
  .cookList li{
       list-style: none;
       width:23%;
       border:1px solid #E5E9F2;
       height: auot;
       overflow: hidden;
       background-color:#fff;
       padding: 2px;
       float:left;
       margin: 2px;

   }
   .cookList li span{

        display: block;
        float:left;
   }
   .foodImg{
       width: 40%;
   }
   .foodName{
       font-size: 18px;
       padding-left: 10px;
       color:brown;

   }
   .foodPrice{
       font-size: 16px;
       padding-left: 10px;
       padding-top:10px;
   }
   .totalDiv{
     background-color: #fff;
     padding: 10px;
     border-bottom: 1px solid #d3dce6;
   }
</style>
