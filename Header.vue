<template>
    <section class="top-header">
        <div class="container">
            <div class="row">
                <div class="col-md-4 col-xs-12 col-sm-4" style="padding-top: 40px">
                    <div class="contact-number glyphicon glyphicon-earphone">
                        <span> 0512-123123-123123</span>
                    </div>
                </div>
                <div class="col-md-4 col-xs-12 col-sm-4 text-center">
                    <router-link to="/"><img @click="jump('/')" src="../assets/images/logo.png" height="70px" alt="">
                    </router-link>
                    <div class="search bar7">
                    </div>
                </div>
                <div class="col-md-4 col-xs-12 col-sm-4" style="padding-top: 0px">
                    <!--搜索框-->
                    <div class="search bar">
                        <form action="" onsubmit="return false">
                            <input placeholder="输入您想要搜索的内容"  v-model="sname" type="text" value="">
                            <button @click="searchAction"></button>
                        </form>
                    </div>
                    <!--登录注册区-->
                    <ul class="top-menu text-right list-inline" v-if="!token">
                        <li class="dropdown cart-nav dropdown-slide">
                            <a href="#" class="dropdown-toggle" data-toggle="dropdown" data-hover="dropdown"><i
                                    class="tf-ion-android-cart"></i>Cart</a>
                            <div class="dropdown-menu cart-dropdown text-center">
                                <!-- Cart Item -->
                                <div class="text-center"><span style="color: red;">请您先登录</span></div>
                            </div>
                        </li><!-- / Cart -->
                        <!--登录-->
                        <li>
                            <router-link to="/login">登录</router-link>
                        </li>
                        |
                        <!--注册-->
                        <li>
                            <router-link to="/register">注册</router-link>
                        </li>
                    </ul><!-- / .nav .navbar-nav .navbar-right -->
                    <ul class="top-menu text-right list-inline" v-else>
                        <li class="dropdown cart-nav dropdown-slide">
                            <a href="#" class="dropdown-toggle" data-toggle="dropdown" data-hover="dropdown"><i
                                    class="tf-ion-android-cart"></i>Cart</a>
                            <div class="dropdown-menu cart-dropdown">
                                <!-- Cart Item -->
                                <div class="media">
                                    <a class="pull-left" href="#">
                                        <img class="media-object" src="images/shop/cart/cart-1.jpg" alt="image"/>
                                    </a>
                                    <div class="media-body">
                                        <h4 class="media-heading"><a href="">Ladies Bag</a></h4>
                                        <div class="cart-price">
                                            <span>1 x</span>
                                            <span>1250.00</span>
                                        </div>
                                        <h5><strong>$1200</strong></h5>
                                    </div>
                                    <a href="#" class="remove"><i class="tf-ion-close"></i></a>
                                </div><!-- / Cart Item -->
                                <!-- Cart Item -->
                                <div class="media">
                                    <a class="pull-left" href="#">
                                        <img class="media-object" src="images/shop/cart/cart-2.jpg" alt="image"/>
                                    </a>
                                    <div class="media-body">
                                        <h4 class="media-heading"><a href="">Ladies Bag</a></h4>
                                        <div class="cart-price">
                                            <span>1 x</span>
                                            <span>1250.00</span>
                                        </div>
                                        <h5><strong>$1200</strong></h5>
                                    </div>
                                    <a href="#" class="remove"><i class="tf-ion-close"></i></a>
                                </div><!-- / Cart Item -->

                                <div class="cart-summary">
                                    <span>Total</span>
                                    <span class="total-price">$1799.00</span>
                                </div>
                                <ul class="text-center cart-buttons">
                                    <li><a href="" class="btn btn-small">View Cart</a></li>
                                    <li><a href="" class="btn btn-small btn-solid-border">Checkout</a></li>
                                </ul>
                            </div>
                        </li><!-- / Cart -->
                        <!--用户名-->
                        <li>
                            <b>{{ username }}</b>
                        </li>
                        |
                        <!--注销-->
                        <li>
                            <a @click="logoutAction">注销</a>
                        </li>
                    </ul><!-- / .nav .navbar-nav .navbar-right -->
                </div>
            </div>
        </div>
    </section>
</template>

<script>
    export default {
        name: "Header",
        data() {
            return {
                token: '',
                username: '',
                sname:'',
                pk_list:[]
            }
        },
        created() {
            this.token = sessionStorage.token || localStorage.token || '';
            this.username = sessionStorage.user_name || localStorage.user_name || ''
        },
        methods: {
            jump(location) {
                this.$router.push(location)
            },
            logoutAction() {
                // 清除登录信息
                sessionStorage.removeItem('token');
                sessionStorage.removeItem('user_name');
                sessionStorage.removeItem('user_mobile');
                localStorage.removeItem('token');
                localStorage.removeItem('user_name');
                localStorage.removeItem('user_mobile');
                this.token = '';
                this.username = ''
            },
            searchAction() {
                if (!this.sname) {
                    sessionStorage.removeItem('s_results')
                }
                this.$axios({
                    url:this.$settings.base_url + '/shoes/search_shoes/',
                    method:'post',
                    data:{
                        content:this.sname
                    },
                }).then(response => {
                    for(let item of response.data.results){
                        this.pk_list.push(item.pk)
                    }
                    sessionStorage.pk_list = this.pk_list
                }).catch(error =>{
                    window.console.log(error)
                });
                this.$router.go(0);
                this.$router.push('/search_shoes');
            }
        }
    }
</script>

<style scoped>
    * {
        box-sizing: border-box;
    }

    div.search {
        padding-top: 10px;
        padding-bottom: 10px;
        padding-right: 0px;
    }

    form {
        position: relative;
        width: 300px;
        margin: 0 auto;
    }

    input, button {
        border: none;
        outline: none;
    }

    input {
        margin-left: 30px;
        width: 100%;
        height: 40px;
        padding-left: 13px;
    }

    button {
        height: 44px;
        width: 42px;
        cursor: pointer;
        position: absolute;
    }

    .bar input {
        border: 2px solid #c5464a;
        border-radius: 5px;
        background: transparent;
        top: 0;
        right: 0;
    }

    .bar button {
        background: #c5464a;
        border-radius: 0 5px 5px 0;
        width: 60px;
        top: 0;
        right: -30px;
    }

    .bar button:before {
        content: "搜索";
        font-size: 13px;
        color: #F9F0DA;
    }
</style>