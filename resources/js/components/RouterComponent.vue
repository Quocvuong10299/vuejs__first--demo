<template>
    <!--<div class="container-fluid top_menu w-100 d-flex">-->
        <!--<div class="container d-flex justify-content-between lex_menu">-->
            <!--<div style="font-size: 24px;font-weight: bold;" class="logo text-white">King's Cake</div>-->
            <!--<nav class="main_menu">-->
                <!--<ul class="__menu w-100 d-flex my-0">-->
                    <!--<li>-->
                        <!--<router-link to="/">Home</router-link>-->
                    <!--</li>-->
                    <!--&lt;!&ndash;<li>&ndash;&gt;-->
                        <!--&lt;!&ndash;<router-link to="/about">About</router-link>&ndash;&gt;-->
                    <!--&lt;!&ndash;</li>&ndash;&gt;-->
                <!--</ul>-->
            <!--</nav>-->
            <!--<div class="right_component">-->
                <!--<div class="search">-->

                <!--</div>-->
                <!--<div class="bag_cart position-relative">-->
                    <!--<i class="fa fa-shopping-bag position-relative" aria-hidden="true">-->
                        <!--<p class="notify_number">20</p>-->
                        <!--&lt;!&ndash;<p class="notify_number">{{pagination.current_page}}</p>&ndash;&gt;-->
                    <!--</i>-->
                    <!--<div class="component_cart shadow-sm p-3 mb-5 bg-white rounded">-->
                        <!--<div class="show_cart">-->
                            <!--<img style="width:70px; height:70px;" src="/image/images.jpeg"/>-->
                            <!--<div class="info_products">-->
                                <!--<p class="font-weight-bold">Apple Watch series 3</p>-->
                                <!--<p><strong>Quantity:</strong> 10</p>-->
                                <!--<p class="mr-1"><strong>Total:</strong> 350$</p>-->
                            <!--</div>-->
                            <!--<i class="fa fa-trash-o" aria-hidden="true"></i>-->
                        <!--</div>-->
                        <!--<hr>-->
                        <!--<div class="show_cart">-->
                            <!--<img style="width:70px; height:70px;" src="/image/images.jpeg"/>-->
                            <!--<div class="info_products">-->
                                <!--<p class="font-weight-bold">Apple Watch series 3</p>-->
                                <!--<p><strong>Quantity:</strong> 10</p>-->
                                <!--<p class="mr-1"><strong>Total:</strong> 350$</p>-->
                            <!--</div>-->
                            <!--<i class="fa fa-trash-o" aria-hidden="true"></i>-->
                        <!--</div>-->
                        <!--<hr>-->
                        <!--<div class="btn_action">-->
                            <!--<button type="button" class="btn btn-danger">Clear All</button>-->
                            <!--<button type="button" class="btn btn-success">Checkout</button>-->
                        <!--</div>-->
                    <!--</div>-->
                <!--</div>-->
            <!--</div>-->
        <!--</div>-->
    <!--</div>-->
</template>
<script>

    export default {}
</script>

<style lang="scss">
    .top_menu{
        background: #000;
        height:65px;
    }
    .lex_menu{
        align-items: center;
    }
    .__menu{
        list-style:none;
        >li{
            margin: 0 60px;
        }
        a{
            color:#fff;
            &:hover{
                text-decoration: none;
            }
        }
    }
    .bag_cart{
        padding: 21px 0;
            &:hover{
                .component_cart{
                    visibility: inherit;
                    opacity: 1;
                    transform: translateY(0);
                }

            }
        >.fa{
            color:#fff;
            font-size:25px;
            cursor: pointer;
        }
        .notify_number{
            width: 20px;
            height: 20px;
            background: red;
            position: absolute;
            top:-10px;
            right:-15px;
            border-radius:100%;
            font-size: 13px;
            display: flex;
            justify-content: center;
            align-items: center;
            text-align: center;
        }
    }

    .component_cart{
        position:absolute;
        right:-90px;
        top:100%;
        width:290px;
        height:max-content;
        z-index: 100;
        padding: 15px;
        visibility: hidden;
        opacity: 0;
        transition: all 0.3s ease-in-out;
        transform: translateY(20px);
        &:before{
            content: "";
            width: 20px;
            height: 20px;
            position: absolute;
            background: #fff;
            top:-6px;
            transform: rotate(45deg);
            right:91px;
        }
    }
    .show_cart{
        overflow: hidden;
        display: flex;
        position: relative;
        .fa{
            font-size:20px;
            padding: 5px;
            &:hover{
                color:red;
                cursor:pointer;
            }
        }
        img{
            margin-right:15px;
        }
    }
    .info_products{
        width: 120px;
    }
</style>
