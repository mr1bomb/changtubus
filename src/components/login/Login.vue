<template>
    <div>
        <v-header></v-header>
        <div class="categories-section main-grid-border" id="mobilew3layouts">
            <div class="container">
                <div>
                    <div class="list">
                        <ul class="resp-tabs-list hor_1">
                            <li @click="search()">查询</li>
                            <li @click="gobuy()">购买</li>
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
                                    杭州电子科技大学18届学生。在web研发，app开发，数据可视化上有兴趣的可以交流。qq：932575726
                                    <br>github:https://github.com/mr1bomb
                                  </div>
                                  <div class="modal-footer">
                                    <button type="button" class="btn btn-default" data-dismiss="modal">关闭</button>
                                  </div>
                                </div>
                              </div>
                            </div>
                          </li>
                            <li id="login" style="color:#409EFF">
                                <span>登录</span>/
                                <span>注册</span>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>

        <div id="logo1" class="resp-tabs-container hor_1">
            <!-- tab1 -->
            <div class="btn">
                <div class="tabs-box">
                    <img src="static/images/mobile.png" class="w3ls-mobile" alt="" data-pin-nopin="true">
                    <ul class="tabs-menu">
                        <li>
                            <label class="radio" style="color:#409EFF">
                                <i style="color:#409EFF"></i>请登录您的账号</label>
                        </li>
                    </ul>
                    <div class="clearfix"> </div>
                    <div class="tab-grids">
                        <div id="tab1" class="tab-grid">
                            <div class="login-form">
                                <form id="signup">
                                    <ol>
                                        <li>
                                            <p id="loginuser" style="color:red"></p>
                                            <h4>请输入您的用户名</h4>
                                          <el-input v-model="logins.username" placeholder="用户名"></el-input>
                                        </li>
                                        <li>
                                            <h4>请输入您的密码</h4>
                                          <el-input v-model="logins.password" placeholder="密码"></el-input>
                                        <li>
                                      <el-button type="primary" @click="login()">确认登录</el-button>
                                        </li>
                                    </ol>
                                </form>
                            </div>
                        </div>
                    </div>
                    <div class="clearfix"> </div>
                </div>
            </div>
        </div>

        <!-- 注册 -->

        <div id="logo2" class="resp-tabs-container hor_1">
            <!-- tab1 -->
            <div class="btn">
                <div class="tabs-box">
                    <ul class="tabs-menu">
                        <li>
                            <label class="radio" style="color:#409EFF">
                                <i></i>注册账号</label>
                        </li>
                    </ul>
                    <p id="reguser" style="color:red"></p>
                    <div class="clearfix"> </div>
                    <div class="tab-grids">
                        <div id="tab1" class="tab-grid">
                            <div class="login-form">
                                <div id="signup">
                                    <ol>
                                        <li>
                                            <h4>请输入您的用户名</h4>
                                          <el-input v-model="user.username" placeholder="用户名"></el-input>
                                        </li>
                                        <li>
                                            <h4>请输入您的密码</h4>
                                          <el-input v-model="user.password" placeholder="密码"></el-input>
                                        </li>
                                        <li>
                                            <h4>请确认您的密码</h4>
                                          <el-input v-model="surepassword" placeholder="确认密码"></el-input>
                                        </li>
                                        <li>
                                            <h4>请输入您的手机号码</h4>
                                          <el-input v-model="user.phone" placeholder="手机号码"></el-input>
                                        </li>
                                        <li>
                                          <el-button type="primary" @click="reg()">确认注册</el-button>
                                        </li>
                                    </ol>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="clearfix"> </div>
                </div>
            </div>
        </div>

        <adv></adv>
        <v-foot></v-foot>
    </div>
</template>

<script>
import router from '../../router'
import $ from 'jquery'
import head from '../head/Head'
import adv from '../adv/Adv'
import foot from '../foot/Foot'

export default {
    data() {
        return {
          user:{
            username:'',
            password:'',
            phone:'',
            question:'q',
            answer:'q'
          },
          surepassword:'',
          logins:{
            username:'',
            password:''
          }
        }
    },
  /*mounted() {
    this.getList();
  },*/
    components: {
        'v-header': head,
        'adv': adv,
        'v-foot': foot
    },
    methods: {
        /*getList(){
            var that = this;
          $.ajax({
            type: 'post',
            url: '/api/version',
            data: {},
            //dataType: "json",
            contentType: "application/json",
            success: function (data) {


            },
            error: function (data) {
              var data = [
                {
                  username: "ShawYu",
                  password: "123456",
                  phone:110,
                },
                {
                  username: "YanZUwu",
                  password: "123456",
                  phone:120,
                },
                {
                  username: "Steve",
                  password: "123456",
                  phone:130,
                }
              ];
              for(var i = 0;i<data.length;i++){
                  that.users.push(data[i]);
              }
            }
          });
        },*/
        login() {
            var that = this;
          $.ajax({
            type: 'post',
           url: 'http://localhost/chepiao/public/index.php/v1/user/login',
            data: this.logins,
            dataType: "json",
            //contentType: "application/json",
            success: function (data) {
              console.log(typeof data);
               if(data.status_code ===0){
                 var sessionstorage = window.sessionStorage;
                 console.log(sessionstorage);
                 sessionstorage.setItem('username', that.logins.username);
                 sessionstorage.setItem('tok', data.token);
                 sessionstorage.setItem('exit', '/退出登录');
                 window.history.back();
               }else{
                 //$("#loginuser").text('用户名或密码错误');
               }
            },
            error: function (data) {
                $("#loginuser").text('用户名或密码错误');
            }
          })
        },
        reg() {
          var that = this;
          if (that.user.username == "" || that.user.password == "") {
            $("#reguser").text('账号和密码不能为空！')
          }
          if (that.user.password !== that.surepassword) {
            $("#reguser").text('两次输入的密码不一致！')
          }else {
            $.ajax({
              type: 'post',
              url: 'http://localhost/chepiao/public/index.php/v1/user',
              data: that.user,
              dataType: "json",
              //contentType: "application/json",
              success: function (data) {
                  //console.log(data);
                if(data.status_code ===0) {
                  alert("注册成功,请登录");
                  location.href = "index.html";
                }else{
                  $("#reguser").text(data.message);
                  //alert(11)
                }
              },
              error: function (data) {
                  //console.log(data);
                $("#reguser").text(data.responseJSON.message);
                  // console.log(data)
              /* var data = {status_code:0,
                 status_msg:'success'};
                if(data.status_code ===0) {
                  alert("注册成功,请登录");
                  location.href = "index.html";
                }else{
                  $("#reguser").text(data.status_msg);
                }*/
              }
            });
          }
            /*var flag = false;
            for (var i = 0, len = this.users.length; i < len; i++) {
                if (this.users[i].username === regusername) {
                    flag = true;
                    $("#reguser").text('该用户名已经被注册！')
                    break;
                }
            }
            if (!flag) {
                if (regusername == "" || regpassword == "") {
                    $("#reguser").text('账号和密码不能为空！')
                }
                if (regpassword !== surepassword) {
                    $("#reguser").text('两次输入的密码不一致！')
                } else {
                    newuser.username = regusername;
                    newuser.password = regpassword;
                    this.users.push(newuser);
                    $("#regusername").val('')
                    $("#regpassword").val('')
                    $("#surepassword").val('')
                    $("#phone").val('')
                    alert("注册成功")
                    location.href = "index.html";
                }
            }*/
        },
        hidden() {
            $("#reguser").text('')
            $("#loginuser").text('')
        },
      /*gobuy(){
        router.push({ name: 'buy' });
      },*/
        search() {
            router.push({ name: 'Homepage' });
        },
        mine() {
            router.push({ name: 'mine' });
        }
    }
}
</script>

<style>
.w3ls-mobile {
    padding-top: 30px;
    padding-right: 30px
}

.info {
    padding: 10px;
    font-weight: normal;
    background: none;
    border: 1px solid #e4e4e4;
    color: #545454;
    outline: none;
    font-size: 14px;
    transition: 0.5s all;
    -webkit-transition: 0.5s all;
    -o-transition: 0.5s all;
    -ms-transition: 0.5s all;
    background: #fff;
    -moz-transition: 0.5s all;
}

#logo1 {
    display: inline-block;
    margin-right: 20%
}

#logo2 {
    display: inline-block;
}
</style>
