<template>
    <div id="app">

        <v-header></v-header>
        <div class="categories-section main-grid-border" id="mobilew3layouts">
            <div class="container">
                <div>
                    <div>
                        <div class="list">
                            <ul class="resp-tabs-list hor_1">
                                <li style="color:#409EFF">查询</li>
                                <li @click="manager()">管理员</li>
                                <li @click="mine()">我的订单</li>
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
                        <div class="resp-tabs-container hor_1" id="cha">
                            <!-- tab1 -->
                            <div>
                                <div class="tabs-box">

                                    <div class="tab-grids">
                                        <div id="tab1" class="tab-grid">
                                            <div class="login-form">
                                                <form id="signup">
                                                    <ol>
                                                        <li>
                                                            <h2>查询</h2>
                                                            <br>
                                                          <el-input style='width: 400px;height:40px' v-model="form.start" placeholder="始发站" required="required"></el-input>
                                                        </li>

                                                        <li>
                                                          <el-input style='width: 400px;height:40px' v-model="form.end" placeholder="终点站" required="required"></el-input>
                                                        </li>

                                                        <li>
                                                            <el-date-picker  style='width: 400px;height:40px'
                                                              v-model="form.date"
                                                              type="date"
                                                              placeholder="选择日期">
                                                            </el-date-picker>
                                                        </li>

                                                        <li>
                                                          <el-button @click="search()" type="primary" style='width: 200px;height:40px'>查询</el-button>
                                                        </li>
                                                    </ol>
                                                </form>
                                            </div>

                                        </div>
                                    </div>

                                </div>

                            </div>

                        </div>
                    </div>
                </div>
            </div>
        </div>
<div id="td" style="display: none">
  <el-table
    :data="tableData3"
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
      prop="time_end"
      label="到达时间"
      width="400">
    </el-table-column>
    <el-table-column
      prop="num"
      label="车票剩余"
      width="200">
    </el-table-column>
    <el-table-column
      prop="price"
      label="价格"
      width="200">
    </el-table-column>
    <el-table-column
      label="点击购买(一次只能买一张，一个账号同一班车次最多可买三张)">
      <template slot-scope="scope">
        <el-button
          @click.native.prevent="deleteRow(scope.$index, tableData3)"
          type="text"
          size="small">
          购买
        </el-button>
      </template>
    </el-table-column>
  </el-table>
</div>
        <adv></adv>
        <v-foot></v-foot>

    </div>
</template>

<script>
import router from '../../router'
import head from '../head/Head'
import adv from '../adv/Adv'
import foot from '../foot/Foot'
import $ from 'jquery'

//this.$store.state
export default {
    data() {
        return {
          tableData3:[],
          //tableData3: [{start:'杭州',end:'上海',time_start:1491789600000,time_end:1494381600000,num:30,price:100},{start:'杭州',end:'上海',time_start:1491789600000,time_end:1494381600000,num:30,price:200}],
            form:{
              start: '',
              end: '',
              date:''
            },
            //v cusername:window.localStorage.getItem('username')
        }
    },
   /* created(){
        if(this.username){
           $("#login").hide()
        }
    },*/
    components: {
        'v-header': head,
        'adv': adv,
        'v-foot': foot
    },
    methods: {
      deleteRow(index, rows) {
        this.$alert('确定购买？', '', {
          confirmButtonText: '确定',
          callback: action => {
              var row = {};
              for(var key in rows[index]){
                  if(key === 'card'||key === 'time_start'){
                      row[key] = rows[index][key]
                  }
              }
            //console.log(row);
            var tok = window.sessionStorage.getItem('tok');
            if(window.sessionStorage.getItem('tok')) {
              $.ajax({
                type: 'post',
                data: row,
                /*headers: {
                  'Authorization': 'Bearer'  +  window.sessionStorage.getItem('tok')

                },*/
                url: 'http://localhost/chepiao/public/index.php/v1/order?token='+tok,
                success: function (data) {
                  if(data.status_code===0){
                    alert('购买成功')
                  }else{
                    alert(data.status_msg)
                  }
                },
                error: function (err) {
                    /*var data = {status_code:0};
                  if(data.status_code===0){
                    alert('购买成功')
                  }else{
                    alert(data.status_msg)
                  }*/
                  //console.log(99);
                  alert(data.status_msg);
                }
              });
              router.push({ name: 'mine' });
            }else{
              alert('请先登陆')
            }
          }
        });
        //console.log(rows[index].time_start);
      },
        format(date, format){
          var o = {
            "M+": date.getMonth() + 1, // month
            "D+": date.getDate(), // day
            "h+": date.getHours(), // hour
            "m+": date.getMinutes(), // minute
            "s+": date.getSeconds(), // second
            "q+": Math.floor((date.getMonth() + 3) / 3), // quarter
            "S": date.getMilliseconds()
            // millisecond
          };
          if (/(Y+)/.test(format)) {
            format = format.replace(RegExp.$1, (date.getFullYear() + "").substr(4 - RegExp.$1.length));
          }
          for (var k in o) {
            if (new RegExp("(" + k + ")").test(format)) {
              format = format.replace(RegExp.$1, RegExp.$1.length == 1 ? o[k] : ("00" + o[k]).substr(("" + o[k]).length));
            }
          }
          return format;
        },
      transDate(time, format) {
        if (!time) {
          return "";
        }
        return this.format(new Date(time), format || 'YYYY-MM-DD hh:mm:ss');
      },
        search(){
          var a=1491789600000;
          var b=1494381600000;
          console.log(this.transDate(this.form.date.getTime()).split(' ')[0]);
          this.form.date=this.transDate(this.form.date.getTime()).split(' ')[0];
           //console.log((b-a)/(60*60*1000));
          // console.log(this.transDate(a));
            document.getElementById('cha').style = 'display:none';
          document.getElementById('td').style = 'display:block';
            var that = this;
          $.ajax({
            type: 'get',
            url: 'http://localhost/chepiao/public/index.php/v1/ticket/'+this.form.date+'/'+this.form.start+'/'+this.form.end,
            //data: this.form,
            dataType: "json",
            //contentType: "application/json",
            success: function (data) {
              if(data.status_code===0&&data.data.length>0){
                  //alert(22);
                that.tableData3 = data.data;
              }else{
                alert('暂无车次');
                document.getElementById('cha').style = 'display:block';
                document.getElementById('td').style = 'display:none';
                that.form.date = '';
                that.form.start = '';
                that.form.end = '';
              }
            },
            error: function (data) {
                //alert(11)
           /* var data = {status_code:0,data:[{card:'g12345',start:'杭州',end:'上海',time_start:'2011-11-11',time_end:'2011-11-11',num:30,price:100},{start:'杭州',end:'上海',time_start:'2011-11-22',time_end:'2011-11-22',num:30,price:200}]};
            if(data.status_code===0){
              that.tableData3 = data.data;
            }else{
                alert('暂无车次');
              document.getElementById('cha').style = 'display:block';
              document.getElementById('td').style = 'display:none';
            }*/
            }
          })
        },
      manager(){
        router.push({ name: 'refund' });
      },
        /*gobuy(start, end) {
            router.push({ name: 'buy', params: { start: start, end: end } })
        },*/
        change() {
            router.push({ name: 'change' });
        },
        mine() {
            router.push({ name: 'mine' });
        },
        gologin() {
            router.push({ name: 'login' })
        }
    }
}
</script>

<style>
.list {
    margin-top: -50px;
    position: relative
}
#login {
    position: absolute;
    top: -3px;
    right: 100px
}
</style>
