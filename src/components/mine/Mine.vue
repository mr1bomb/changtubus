<template>
    <div>
        <v-header></v-header>

        <!--{{train_no}}--{{start}}--{{end}}--{{start_time}}--{{end_time}}--{{run_time}}-->
        <!-- //breadcrumbs -->
        <div class="categories-section main-grid-border" id="mobilew3layouts">
            <div class="container">
                <div>
                    <div class="list">
                        <ul class="resp-tabs-list hor_1">
                            <li @click="search()">查询</li>
                            <li @click="gogu()">管理员</li>
                            <li>我的订单</li>
                          <li style="margin-top: -10px;margin-left: -20px"><button type="button" class="btn btn-default" style="padding:0;width: 200px;height: 50px;border: 1px solid #ffffff;font-size: 20px" data-toggle="modal" data-target="#myModal">
                            <span style="padding: -10px">关于我们</span>
                          </button>

                            <!-- Modal -->
                            <div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel">
                              <div class="modal-dialog" role="document">
                                <div class="modal-content">
                                  <div class="modal-header">
                                    <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
                                    <h4 class="modal-title" id="myModalLabel">冯家乐</h4>
                                  </div>
                                  <div class="modal-body">
                                    杭州电子科技大学18届学生，在web研发，app开发，数据可视化上有兴趣的可以交流。qq：932575726
                                    <br>github:https://github.com/mr1bomb
                                  </div>
                                  <div class="modal-footer">
                                    <button type="button" class="btn btn-default" data-dismiss="modal">关闭</button>
                                  </div>
                                </div>
                              </div>
                            </div>
                          </li>
                            <li id="login" @click="gologin()">
                                <span>登录</span>/
                                <span>注册</span>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
        <!-- Trains -->
      <!-- <div class="agile-trains w3layouts-content">
           <div class="container">
               <div class="col-md-4 bann-info1">

               </div>
               <div class="col-md-5 bann-info" :hidden="myticket">
                   <h3>我的订单</h3>
                   <div class="book-a-ticket">
                       <div class=" bann-info">

                           <div class="box">
                               <div class="start">
                                   <h2>{{start}}</h2>
                               </div>
                               <span class="train_no">
                                   <h3>{{train_no}}</h3>
                               </span>
                               <div class="arrow">

                                   <img src="./arrow.png" width="20%" height="20%">
                               </div>
                               <div class="end">
                                   <h2>{{end}}</h2>
                               </div>
                               <div class="time">
                                   <span class="time_">
                                       <h3>出发</h3>
                                   </span>
                                   <span class="time_">
                                       <h3>到达</h3>
                                   </span>
                                   <span class="time_">
                                       <h3>历时</h3>
                                   </span>
                               </div>
                               <div class="num">
                                   <span class="num_">
                                       <h3>{{start_time}}</h3>
                                   </span>
                                   <span class="num_">
                                       <h3>{{end_time}}</h3>
                                   </span>
                                   <span class="num_">
                                       <h3>{{run_time}}</h3>
                                   </span>
                               </div>
                               <div class="clearfix"></div>
                               <div class="search">
                                   <input type="submit" class="submit" value="退票" @click="refund()">
                                   <input type="submit" class="submit" value="改签" @click="change()">
                               </div>

                           </div>

                       </div>
                   </div>

                </div>
                <div class="clearfix"></div>
                <h3 :hidden="gobuy" class="hh3">您还没有订单哦 赶快去购票吧~</h3>
            </div>
        </div>-->
      <div style="font-size: 24px;margin-bottom: 20px">我的订单</div>
      <el-table
        :data="tableData4"
        height="250"
        border
        style="width: 100%">
        <el-table-column
          prop="card"
          label="车牌号"
          width="200">
        </el-table-column>
        <el-table-column
          prop="start"
          label="始发站"
          width="200">
        </el-table-column>
        <el-table-column
          prop="end"
          label="终点站"
          width="200">
        </el-table-column>
        <el-table-column
          prop="time_start"
          label="发车时间"
          width="400">
        </el-table-column>
        <el-table-column
          prop="time"
          label="是否已发车"
          width="400">
        </el-table-column>
        <el-table-column
          prop="buy_num"
          label="已购买车票数量"
          width="200">
        </el-table-column>
        <el-table-column
          prop="price"
          label="单张价格"
          width="200">
        </el-table-column>
        <el-table-column
          label="退票，每次点击只允许退一张，直到退完">
          <template slot-scope="scope">
            <el-button
              @click.native.prevent="refund(scope.$index, tableData4)"
              type="text"
              size="small">
              退票
            </el-button>
          </template>
        </el-table-column>
      </el-table>
        <adv></adv>
        <v-foot></v-foot>
    </div>
</template>

<script>
import router from '../../router'
import head from '../head/Head'
import adv from '../adv/Adv'
import foot from '../foot/Foot'

export default {
    data() {
        return {
          tableData4:[],
            /*train_no:this.$store.state.train_no,
            start:this.$store.state.start_station,
            end:this.$store.state.end_station,
            end_time:this.$store.state.end_time,
            start_time:this.$store.state.start_time,
            run_time:this.$store.state.run_time*/
            /*train_no: '',
            start: '',
            end: '',
            end_time: '',
            start_time: '',
            run_time: '',
            myticket: false,
            gobuy: true*/
        }
    },
    mounted() {
      var sessionstorage = window.sessionStorage;
      if(window.sessionStorage.getItem('tok')) {
        this.dingdan()
      }else{
          alert('请先登陆')
      }
      /*  var train__no = localstroage.getItem('train_no');
        var start__station = localstroage.getItem('start_station');
        var end__station = localstroage.getItem('end_station');
        var end__time = localstroage.getItem('end_time');
        var start__time = localstroage.getItem('start_time');
        var run__time = localstroage.getItem('run_time');
        this.train_no = train__no;
        this.start = start__station;
        this.end = end__station;
        this.end_time = end__time;
        this.start_time = start__time;
        this.run_time = run__time;*/
    },
    components: {
        'v-header': head,
        'adv': adv,
        'v-foot': foot
    },
    methods: {
      gogu(){
        router.push({ name: 'refund' });
},
        dingdan(){
          var that = this;
          var tok = window.sessionStorage.getItem('tok');
          $.ajax({
            type: 'get',
           /* headers: {
              'Authorization': 'Bearer'  +  window.sessionStorage.getItem('tok')

            },*/
            url: 'http://localhost/chepiao/public/index.php/v1/order?token='+tok,
            /*data: {token:tok},*/
            dataType: "json",
            success: function (data) {
              if(data.status_code===0){
                  //alert(2);
                for(var i = 0;i<data.data.length;i++){
                  if(data.data[i].time===0){
                    //alert(33)
                    data.data[i].time='未发车'
                  }else if(data.data[i].time===1){
                    data.data[i].time='已发车'
                  }else{
                    data.data[i].time='十分抱歉，因某些特殊原因，该车次被迫取消，请您及时退票，谢谢'
                  }
                }
                that.tableData4 = data.data;
              }
            },
            error: function (err) {
              /*var data = {status_code:0,data:[{card:'q12334',start:'杭州',end:'上海',time_start:'2011-11-11',time_end:'2011-11-11',buy_num:1,price:100},{start:'杭州',end:'上海',time_start:'2011-11-22',time_end:'2011-11-22',buy_num:1,price:200}]}
              if(data.status_code===0){
                that.tableData4 = data.data;
              }*/
             // console.log(99);
            }
          })
        },
        refund(index, rows) {
          this.$alert('确定退票？', '', {
            confirmButtonText: '确定',
            callback: action => {
              var row = {};
              for(var key in rows[index]){
                if(key === 'card'||key === 'time_start'){
                  row[key] = rows[index][key]
                }
              }
              console.log(row);
              var tok = window.sessionStorage.getItem('tok');
              if(window.sessionStorage.getItem('tok')) {
                  var that = this;
                $.ajax({
                  type: 'post',
                 /* headers: {
                    "Content-Type": "application/json",
                    "X-HTTP-Method-Override": "PUT" }, //PUT,DELETE*/
                  data: row,
                  /*headers: {
                    'Authorization': 'Bearer'  +  window.sessionStorage.getItem('tok')

                  },*/
                  //contentType: "application/x-www-form-urlencoded",

                  url: 'http://localhost/chepiao/public/index.php/v1/order/reduce?token='+tok,
                  success: function (data) {
                    if(data.status_code===0){
                      alert('退票成功');
                      that.dingdan();
                    }else{
                      alert(data.status_msg)
                    }
                  },
                  error: function (err) {
                  /*  var data = {status_code:0};
                    if(data.status_code===0){
                      alert('退票成功')
                    }else{
                      alert(data.status_msg)
                    }
                    console.log(99);*/
                  }
                });
                router.push({ name: 'mine' });
              }else{
                alert('请先登陆')
              }
            }
          });
        },
        change() {
            router.push({ name: 'change' });
        },
        search(){
            router.push({ name: 'Homepage' });
        },
        gologin(){
            router.push({ name: 'login' })
        }
    }
}
</script>

<style>
.box {
    position: relative;
    width: 100%;
    height: 500px;
    border: 2px #000 solid;
    margin-top: 20px
}

.w3layouts-content{
    margin-top: -100px
}

.start {
    float: left;
    margin: 50px
}

.end {
    float: right;
    margin: 50px
}

.arrow {
    position: absolute;
    left: 10px;
    top: 70px
}

.train_no {
    position: absolute;
    left: 44%;
    top: 12%
}

.time {
    position: absolute;
    left: 8%;
    bottom: 25%
}

.time_ {
    margin: 25px
}

.num {
    position: absolute;
    right: 8%;
    bottom: 25%
}

.num_ {
    margin: 25px
}

.search {
    position: absolute;
    bottom: 5%;
    left: 22%;
}

.submit {
    margin: 30px
}

.hh3 {
    margin-top: -100px
}
</style>
