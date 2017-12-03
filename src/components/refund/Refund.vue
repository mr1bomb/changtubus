<template>
  <div>
    <v-header></v-header>
    <div class="categories-section main-grid-border" id="mobilew3layouts">
      <div class="container">
        <div>
          <div class="list">
            <ul class="resp-tabs-list hor_1">
              <li @click="search()">查询</li>
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
      login:{
        username: '',
        password: '',
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
    search(){
      router.push({ name: 'Homepage' });
    },
    mine() {
      router.push({ name: 'mine' });
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
            //$("#loginuser").text('用户名或密码错误');
          }
        },
        error: function (data) {
          alert(data.message);
        }
      })
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
