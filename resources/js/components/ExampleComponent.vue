<template>
    <div class="wrapper w-100">
        <!--<RouterComponent></RouterComponent>-->
        <div class="main w-100">
            <router-view>
                <HomeComponent/>
            </router-view>
        </div>
            <FooterComponent></FooterComponent>
    </div>
</template>
<script>
    import RouterComponent from "./RouterComponent";
    import HomeComponent from "./HomeComponent";
    import FooterComponent from "./FooterComponent";
    export default {
        components:{
            RouterComponent,
            FooterComponent,
            HomeComponent
        }
    }
</script>
