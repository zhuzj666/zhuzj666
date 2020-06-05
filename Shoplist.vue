<template>
    <section class="products section">
            <div class="container">
                <div class="row">
                    <div class="col-md-4" v-for="good in good_list" :key="good.pk">
                        <div class="product-item">
                            <div class="product-thumb">
                                <img class="img-responsive" :src="'http://127.0.0.1:8000/media/'+good.img"
                                     alt="product-img"/>
                            </div>
                            <div class="product-content">
                                <h4><a href="" @click="JumpAcition(good.pk)">{{good.name}}</a></h4>
                                <p class="price">￥{{good.price}}起</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>
</template>

<script>
    export default {
        name: "Shoplist",
        data(){
            return{
                pk_list:sessionStorage.pk_list,
                good_list:[]
            }
        },
        created(){
            this.$axios({
                url: this.$settings.base_url + '/shoes/search_result/',
                method: 'post',
                data: {
                    pk_list: this.pk_list,
                },
            }).then(response => {
                this.good_list = response.data.results
            })
        }
    }
</script>

<style scoped>

</style>