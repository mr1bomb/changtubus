<template>
  <div>
    <v-header></v-header>
    <div class="categories-section main-grid-border" id="mobilew3layouts">
      <div class="container">
        <div>
          <div class="list">
            <ul class="resp-tabs-list hor_1">
              <li @click="searchs()">查询</li>
              <li >管理员</li>
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
        </div>
      </div>
    </div>
<div id='guli' style='display:none'>
  <div style="font-size: 24px;margin-right: 10%">管理员添加车次</div>
  <ol style="list-style:none;width:30%;margin-left: 30%" id="gu">
    <li>
      <el-input v-model="user.card" placeholder="请输入车牌号"></el-input>
    </li>
    <li>
      <el-input v-model="user.start" placeholder="请输入始发站"></el-input>
    </li>
    <li>
      <el-input v-model="user.end" placeholder="请输入终点"></el-input>
    </li>
    <li>
      <div class="block" style="width:100%">
        <el-date-picker
          v-model="user.time_start"
          type="datetime"
          placeholder="请输入发车时间">
        </el-date-picker>
      </div>
    </li>
    <li>
      <div class="block" style="width:100%">
        <el-date-picker
          v-model="user.time_end"
          type="datetime"
          placeholder="请输入到达时间">
        </el-date-picker>
      </div>
    </li>
    <li>
      <el-input v-model="user.num" placeholder="请输入总票数"></el-input>
    </li>
    <li>
      <el-input v-model="user.price" placeholder="请输入价格"></el-input>
    </li>
    <li>
      <el-button type="primary" @click="tijiao()">确认提交</el-button>
    </li>
  </ol>
    <form id="signups">
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
    <div id="tds" style="display: none">
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
          label="取消该车次">
          <template slot-scope="scope">
            <el-button
              @click.native.prevent="refunds(scope.$index, tableData4)"
              type="text"
              size="small">
              取消
            </el-button>
          </template>
        </el-table-column>
      </el-table>
    </div>
    <form id="sign">
      <ol>
        <li style="list-style:none">
          <h2>管理员登陆</h2>
          <br>
          <el-input style='width: 400px;height:40px' v-model="login.username" placeholder="管理员用户" required="required"></el-input>
        </li>

        <li style="margin-top: 20px;list-style:none">
          <el-input style='width: 400px;height:40px' v-model="login.password" placeholder="管理员密码" required="required"></el-input>
        </li>

        <li style="margin-top: 20px;list-style:none">
          <el-button @click="lo" type="primary" style='width: 200px;height:40px'>登陆</el-button>
        </li>
      </ol>
    </form>

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
      login:{
        username: '',
        password: '',
      },form:{
        start: '',
        end: '',
        date:''
      },
user:{
  card:'',
  start:'',
  end:'',
  time_start:'',
  time_end:'',
  num:'',
  price:''
}
    }
  },
  components: {
    'v-header': head,
    'adv': adv,
    'v-foot': foot
  },
  methods: {
    searchs(){
      router.push({ name: 'Homepage' });
    },
    mine() {
      router.push({ name: 'mine' });
    },
    refunds(index, rows) {
      this.$alert('确定取消？', '', {
        confirmButtonText: '确定',
        callback: action => {
          var row = {};
          for(var key in rows[index]){
            if(key === 'card'){
              row[key] = rows[index][key]
            }if(key === 'time_start'){
              row[key] = rows[index][key];
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

              url: 'http://localhost/chepiao/public/index.php/v1/ticket/del?token='+tok,
              success: function (data) {
                if(data.status_code===0){
                  alert('取消车次成功');

                 // that.dingdan();
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
            document.getElementById('guli').style = 'display:block';
            document.getElementById('signups').style = 'display:block';
            document.getElementById('tds').style = 'display:none';
            this.form.start = '';
            this.form.end = '';
            this.form.date = '';
            this.user.card = '';
            this.user.start = '';
            this.user.end = '';
            this.user.time_start = '';
            this.user.time_end = '';
            this.user.num = '';
            this.user.price = '';
            //router.push({ name: 'mine' });
          }else{
            alert('请先登陆')
          }
        }
      });
    },
    tijiao(){
      var that = this;
      this.user.time_start = this.transDate(this.user.time_start);
      this.user.time_end = this.transDate(this.user.time_end);
      console.log(this.user);
      var tok = window.sessionStorage.getItem('tok');
      $.ajax({
        type: 'post',
        url: 'http://localhost/chepiao/public/index.php/v1/ticket?token='+tok,
        data: this.user,
        /*headers: {
          'Authorization': 'Bearer'  +  window.sessionStorage.getItem('tok')

        },*/
        dataType: "json",
        //contentType: "application/json",
        success: function (data) {
          if(data.status_code ===0){
            alert('添加成功');
          }else{
            alert(data.message);
            //$("#loginuser").text('用户名或密码错误');
          }
        },
        error: function (data) {
          alert(data.message);
        }
      });
      this.user.card = '';
      this.user.start = '';
      this.user.end = '';
      this.user.time_start = '';
      this.user.time_end = '';
      this.user.num = '';
      this.user.price = '';
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
      document.getElementById('signups').style = 'display:none';
      document.getElementById('guli').style = 'display:none';
      document.getElementById('tds').style = 'display:block';
      //console.log((b-a)/(60*60*1000));
      // console.log(this.transDate(a));
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
            that.tableData4 = data.data;
          }else{
            alert('暂无车次');
            document.getElementById('guli').style = 'display:block';
            document.getElementById('signups').style = 'display:block';
            document.getElementById('tds').style = 'display:none';
            that.form.start = '';
            that.form.end = '';
            that.form.date = '';
            that.user.card = '';
            that.user.start = '';
            that.user.end = '';
            that.user.time_start = '';
            that.user.time_end = '';
            that.user.num = '';
            that.user.price = '';
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
    lo() {
      var that = this;
      $.ajax({
        type: 'post',
        url: 'http://localhost/chepiao/public/index.php/v1/root/login',
        data: this.login,
        dataType: "json",
        //contentType: "application/json",
        success: function (data) {
          if(data.status_code ===0){
              alert('登陆成功');
            var sessionstorage = window.sessionStorage;
            //console.log(sessionstorage);
            sessionstorage.setItem('tok', data.token);
            sessionstorage.setItem('username', that.login.username);
            console.log(window.sessionStorage.getItem('tok'));
            sessionstorage.setItem('exit', '/退出登录');
            document.getElementById('sign').style='display:none';
            document.getElementById('guli').style='display:block'
          }else{
            alert('用户名或密码错误');
          }
        },
        error: function (data) {
          alert('用户名或密码错误');
        }
      })
    },
  }
}
</script>

<style>
  #signups{
    margin-left: -220px;
  }
  #signups li{
    list-style-type: none;
    margin-top: 20px;
  }

#gu li{
  height: 60px;
  margin-top:20px;
}
#gu .el-input input{
  height:55px;
}
.el-date-editor.el-input, .el-date-editor.el-input__inner{
    width:100%
  }
</style>
