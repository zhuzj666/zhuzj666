<template>
    <section class="page-header">
        <div class="container">
            <div class="row">
                <div class="col-md-12">
                    <div class="content">
                        <h1 class="page-name">Air Jordan{{c_id}}</h1>
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
        name: "PageHeader1",
		data(){
            return {
                c_id:sessionStorage.cate
            }
        }
    }
</script>

<style scoped>

</style>