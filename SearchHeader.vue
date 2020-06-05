<template>
    <section class="page-header">
        <div class="container" v-if="!pk_list">
            <div class="row">
                <div class="col-md-12">
                    <div class="content">
                        <h1 class="page-name">暂无查询结果</h1>
                        <ol class="breadcrumb">
                        </ol>
                    </div>
                </div>
            </div>
        </div>
        <div class="container" v-else>
            <div class="row">
                <div class="col-md-12">
                    <div class="content">
                        <h1 class="page-name">查询结果</h1>
                        <ol class="breadcrumb">
                            <li>Love</li>
                            <li>Peace</li>
                        </ol>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
    export default {
        name: "SearchHeader",
        data() {
            return {
                pk_list: sessionStorage.pk_list
            }
        },
        created(){
            window.console.log(this.pk_list)
        }
    }
</script>

<style scoped>

</style>