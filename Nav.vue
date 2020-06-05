<template>
    <section>
        <nav class="navbar navigation" style="margin-bottom: 0px">
            <div class="container">
                <!-- Navbar Links -->
                <div class="navbar-collapse collapse text-center">
                    <ul class="nav navbar-nav">
                        <!-- Home -->

                        <li>
                            <a href=""  @click="jumpAction('/')"><b>Home</b></a>
                        </li>
                        <li>
                            <a href=""  @click="jumpAction('/aj1/',1)"><b>AirJordan1</b></a>
                        </li>
                        <li>
                            <a href=""  @click="jumpAction('/aj4/',4)"><b>AirJordan4</b></a>
                        </li>
                        <li>
                            <a href=""  @click="jumpAction('/aj5/',5)"><b>AirJordan5</b></a>
                        </li>
                        <li>
                            <a href=""  @click="jumpAction('/aj6/',6)"><b>AirJordan6</b></a>
                        </li>
                        <li>
                            <a href=""  @click="jumpAction('/aj11/',11)"><b>AirJordan11</b></a>
                        </li>
                    </ul>
                </div>
            </div><!-- / .container -->
        </nav>
    </section>
</template>

<script>
    export default {
        name: "Nav",
        methods: {
            jumpAction(router,c_id){
                sessionStorage.cate = c_id;
                this.$router.push(router)
            }
        }
    }
</script>

<style scoped>

</style>