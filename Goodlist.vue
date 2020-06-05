<template>
    <section class="products section bg-gray">
    <div class="container">
        <div class="row">
            <div class="title text-center">
                <h3>人气新品</h3>
            </div>
        </div>
        <div class="row">

            <div class="col-md-4" v-for="(data,index) in datalist" :key="data.name">
                <div class="product-item">
                    <div class="product-thumb">
                        <img class="img-responsive" :src="'http://127.0.0.1:8000/media/'+data.img" alt="product-img"/>
                        <div class="preview-meta">
                            <ul>
                                <li>
									<span data-toggle="modal" :data-target="'#product-modal'+index">
										<i class="tf-ion-ios-search-strong"></i>
									</span>
                                </li>
                            </ul>
                        </div>
                    </div>
                    <div class="product-content">
                        <h4><a href="" @click="JumpAcition(data.pk)">{{data.name}}</a></h4>
                        <p class="price">￥{{data.price}}起</p>
                    </div>
                </div>
            </div>
            <div class="modal product-modal fade" v-for="(data,index) in datalist" :id="'product-modal'+index" :key="index">
                <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                    <i class="tf-ion-close"></i>
                </button>
                <div class="modal-dialog " role="document">
                    <div class="modal-content">
                        <div class="modal-body">
                            <div class="row">
                                <div class="col-md-8 col-sm-6 col-xs-12">
                                    <div class="modal-image">
                                        <img class="img-responsive"  :src="'http://127.0.0.1:8000/media/'+data.img"  style="width: 430px"
                                             alt="product-img"/>
                                    </div>
                                </div>
                                <div class="col-md-4 col-sm-6 col-xs-12">
                                    <div class="product-short-details">
                                        <h2 class="product-title">{{data.name}}</h2>
                                        <p class="product-price">￥{{data.price}}起</p>
                                        <p class="product-short-description">
                                            {{data.desc}}
                                        </p>
                                        <button class="btn btn-success" @click="JumpAcition(data.pk)">查看详情</button>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>


        </div>
    </div>
</section>

</template>

<script>
    export default {
        name: "Goodlist",
        data() {
            return {
                datalist:[],
    };
        },
        created(){
            this.$axios({
                url:this.$settings.base_url+'/shoes/new_shoes/',
                method:'get',
            }).then(response=>{
                window.console.log(response.data);
                this.datalist = response.data.results
            })
        },
        methods: {
            JumpAcition(pk){
                sessionStorage.pk = pk ;
                this.$router.push('/good_detail/');
                this.$router.go(0);
            },
        }
    }

</script>

<style scoped>

</style>