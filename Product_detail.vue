<template>
    <section class="single-product">
        <div class="container">
            <div class="row">
                <div class="col-md-6">
                    <ol class="breadcrumb">
                        <li><a href="#">Home</a></li>
                        <li><a href="#">Shop</a></li>
                        <li class="active">Single Product</li>
                    </ol>
                </div>
            </div>
            <div class="row mt-20">
                <div class="col-md-5">
                    <div class="single-product-slider">
                        <div id='carousel-custom' class='carousel slide' data-ride='carousel'>
                            <div class='carousel-outer'>
                                <!-- me art lab slider -->
                                <div class='carousel-inner'>
                                    <div class='item active'>
                                        <img-zoom :src="'http://127.0.0.1:8000/media/'+first_img" width="430" height="430" :bigsrc="'http://127.0.0.1:8000/media/'+first_img" :configs="configs"></img-zoom>
                                    </div>
                                    <div class='item' v-for="img in img_list" :key="img.shoe_img">
                                        <img-zoom :src="'http://127.0.0.1:8000/media/'+img.shoe_img" width="430" height="430" :bigsrc="'http://127.0.0.1:8000/media/'+img.shoe_img" :configs="configs"></img-zoom>
                                    </div>
                                </div>

                                <!-- sag sol -->
                                <a class='left carousel-control' href='#carousel-custom' data-slide='prev'>
                                    <i class="tf-ion-ios-arrow-left"></i>
                                </a>
                                <a class='right carousel-control' href='#carousel-custom' data-slide='next'>
                                    <i class="tf-ion-ios-arrow-right"></i>
                                </a>
                            </div>

                            <!-- thumb -->
                            <ol class='carousel-indicators mCustomScrollbar meartlab'>
                                <li data-target='#carousel-custom' data-slide-to='0' class='active'>
                                    <img :src="'http://127.0.0.1:8000/media/'+first_img" alt=''/>
                                </li>
                                <li data-target='#carousel-custom' :data-slide-to='index+1'
                                    v-for="(img,index) in img_list" :key="img.shoe_img">
                                    <img :src="'http://127.0.0.1:8000/media/'+img.shoe_img" alt=''/>
                                </li>

                            </ol>
                        </div>
                    </div>
                </div>
                <div class="col-md-7">
                    <div class="single-product-details">
                        <h2>{{name}}</h2>
                        <p v-if="!now_price" class="product-price" style="font-size: x-large;color: red">
                            <b>￥{{price}}起</b></p>
                        <p v-else class="product-price" style="font-size: x-large; color: red"><b>￥{{now_price}}</b></p>

                        <p class="product-description mt-20">
                            {{desc}}
                        </p>

                        <div class="product-size">
                            <span>鞋码:</span>
                            <select style="width: 65px; height: 35px; text-align: center" @blur="checkStock"
                                    v-model="value" @change="selectAction">
                                <option value="" disabled selected>请选择</option>
                                <option v-for="(size,index) in size_list" :key="size.shoe_size" :value="index">
                                    {{size.shoe_size}}
                                </option>
                            </select>
                        </div>
                        <div class="product-quantity">
                            <span>购买数量:</span>
                            <div class="product-quantity-slider">
                                <input style="width: 50px; text-align: center; margin-right: 50px" v-model="stock"
                                       @blur="checkStock" onkeyup="value=value.replace(/[^\d]/g,'')" type="number"
                                       value="0" min="0"
                                       :max="count" step="1" name="product-quantity">
                            </div>
                            <span v-if="count">库存:{{count}}</span>
                        </div>
                        <div style="margin-top: 80px">
                            <button class="btn" style="color: red ;background-color: rgb(255,237,237); width: 180px">
                                <span style="font-size: large;">立即购买</span>
                            </button>
                            <button class="btn"
                                    style="margin-left: 20px; color: white ;background-color: rgb(255,0,54); width: 180px">
                                <span style="font-size: large;">加入购物车</span>
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
    import imgZoom from 'vue2.0-zoom'
    export default {
        name: "Good_detail",
        components: {
          imgZoom
        },
        data() {
            return {
                stock: '',
                name: '',
                desc: '',
                price: '',
                now_price: '',
                count: '',
                size_list: '',
                img_list: '',
                value: '',
                first_img: '',
                big_img: '../assets/images/aj1黑紫脚趾b.jpg',
                configs: {
                    width: 300,
                    height: 300,
                    maskWidth: 100,
                    maskHeight: 100,
                    maskColor: 'black',
                    maskOpacity: 0.2,
                    scale:3
                }
            }
        },
        methods: {
            selectAction() {
                window.console.log(this.value);
                this.now_price = this.size_list[this.value].price;
                this.count = this.size_list[this.value].count
            },
            checkStock() {
                if (this.stock > this.count) {
                    this.$message.error('您所填写的商品数量超过库存！');
                    return false
                }
            },
        },
        created() {
            let pk = sessionStorage.pk;
            this.$axios({
                url: this.$settings.base_url + '/shoes/shoe_detail/',
                method: 'post',
                data: {
                    pk: pk
                },
            }).then(response => {
                // window.console.log(response);
                this.name = response.data.results.name;
                this.price = response.data.results.price;
                this.desc = response.data.results.desc;
                this.size_list = response.data.results.size_list;

                // window.console.log(response.data.results.img_list);
                this.first_img = response.data.results.img_list.shift().shoe_img;
                this.img_list = response.data.results.img_list;
                window.console.log(this.img_list)
            })
        }
    }
</script>

<style scoped>

</style>