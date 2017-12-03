<template>
    <div>
        <header>
            <div class="container">
                <!--logo-->
                <div class="logo">
                    <h1>
                        <a href="index.html" style="color:#409EFF">长三角长途客车售票网</a>
                    </h1>
                </div>
                <!--//logo-->
                <div class="w3layouts-login">
                    <a data-toggle="modal" data-target="#myModal" href="#" style="color:#409EFF;font-size: 18px">
                         <span>{{myname}}</span><span @click="out()" id="exit">{{exit}}</span>
                    </a>
                </div>
            </div>
        </header>

        <div class="header-right">
            <div class="banner">
                <div class="slider">
                    <div class="callbacks_container">
                        <ul class="rslides" id="slider">
                            <li>
                                <div class="banner1">
                                    <div class="caption">
                                      <h3>
                                        让您的出行不再是难题</h3>
                                    </div>
                                </div>
                            </li>
                            <li>
                                <div class="banner2">
                                    <div class="caption">
                                        <h3>
                                            网上购票，立刻打折</h3>
                                    </div>
                                </div>
                            </li>
                            <li>
                                <div class="banner3">
                                    <div class="caption">


                                        <p>

                                        </p>
                                    </div>
                                </div>
                            </li>
                            <li>
                                <div class="banner4">
                                    <div class="caption">
                                        <h3>
                                        </h3>
                                        <p>

                                        </p>
                                    </div>
                                </div>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import router from '../../router'
import $ from 'jquery'

export default {
    data() {
        return {
            myname: "",
            exit:""
        }
    },
    created(){
        this.myname = window.sessionStorage.getItem('username')
        this.exit = window.sessionStorage.getItem('exit')
    },
    methods: {
        gobuy() {
            router.push({ name: 'buy' });
        },
        out(){
        //利用对话框返回的值 （true 或者 false）  s
        if (confirm("你确定退出吗？")) {
            window.sessionStorage.clear('username','exit')
            window.location="index.html"
        }
     }
    }
}
</script>

<style>
.header-right {
    margin-top: -70px
}
</style>
