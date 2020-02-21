<template>
    <div class="group_components">
        <div class="container-fluid top_menu w-100 d-flex">
            <div class="container d-flex justify-content-center lex_menu">
                <div style="font-size: 24px;font-weight: bold;" class="logo text-white">King's Cake</div>
                <nav class="main_menu">
                    <ul class="__menu w-100 d-flex my-0">
                        <!--<li>-->
                        <!--<router-link to="/">Home</router-link>-->
                        <!--</li>-->
                    </ul>
                </nav>
                <div class="right_component">
                    <div class="search">

                    </div>
                    <div class="bag_cart position-relative">
                        <i class="fa fa-shopping-bag position-relative" aria-hidden="true">
                                <p v-if="getItemTotal" class="notify_number">{{getItemTotal}}</p>
                                <p v-else="" class="notify_number">0</p>
                        </i>
                        <div class="component_cart shadow-sm p-3 mb-5 bg-white rounded">
                            <div v-for="(cart, i) in carts" :key="cart.id"
                                 class="show_cart d-flex justify-content-around">
                                <div class="img_cart">
                                    <img style="width:50px; height:50px;" :src="'/image/product/' + cart.image"/>
                                </div>
                                <div class="info_products">
                                    <p class="font-weight-bold">{{cart.name}}</p>
                                    <!--<p><strong>Quantity:</strong>{{cart.promotion_price > 0 ? cart.promotion_price : cart.unit_price}} x {{cart.qty}}</p>-->
                                    <p><strong>Quantity:</strong>{{cart.qty}}</p>
                                    <div class="input_group">
                                        <input v-model="cart.qty" type="number" min="1" max="200" value="1"/>
                                    </div>
                                </div>

                                <div class="remove">
                                    <i @click="removeCart(i)" class="fa fa-trash-o" aria-hidden="true"></i>
                                </div>
                                <!--<button @click="removeCart(i)" class="btn btn-danger">delete</button>-->
                            </div>
                            <hr>
                            <div v-if="getItemTotal > 0" class="btn_action">
                                <button @click="clearAllCart" type="button" class="btn btn-danger">Clear All</button>
                                <button type="button" class="btn btn-success">Checkout</button>
                                <p style="font-size: 18px;" class="mr-1 d-flex justify-content-center py-2"><strong>Total: </strong>$
                                    {{getSubtotal}}</p>
                            </div>
                            <div class="noti">
                                <h5 v-if="getItemTotal === 0">Cart is empty <i class="fa fa-frown-o" aria-hidden="true"></i></h5>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="container w-100">
            <div class="row">
                <div v-for="product in products" :key="product.id"
                     class="show col-md-4 col-xs-12 col-lg-4 col-sm-4 text-center mt-5">
                    <img :src="'/image/product/' + product.image"/>
                    <h5>{{product.name}}</h5>
                    <div class="price d-flex justify-content-center">
                        <span v-if="product.promotion_price > 0"
                              class="unit_price has_pro px-2">${{product.unit_price}}</span>
                        <h5 v-if="product.promotion_price === 0" class="promotion_price">${{product.unit_price}}</h5>
                        <h5 v-else="" class="promotion_price">${{product.promotion_price}}</h5>
                    </div>
                    <button type="button" class="btn btn-success">Detail</button>
                    <button @click="addCart(product)" type="button" class="btn btn-success">Add to cart</button>
                </div>
            </div>
            <div class="component d-flex justify-content-center mt-5">
                <!--pagination using ajax -->
                <paginate v-if="pagination.current_page > 0"
                          :pageCount="pagination.last_page"
                          :containerClass="'pagination'"
                          :page-class="'page-item'"
                          :page-link-class="'page-link'"
                          :prev-class="'page-item'"
                          :prev-link-class="'page-link'"
                          :next-class="'page-item'"
                          :next-link-class="'page-link'"
                          :prev-text="'<<'"
                          :next-text="'>>'"
                          :first-last-button="false"
                          :clickHandler="clickCallback">
                </paginate>
            </div>
        </div>
    </div>
</template>
<script>
    import Paginate from 'vuejs-paginate';

    export default {
        components: {
            Paginate
        },
        data() {
            return {
                products: [],
                product: {
                    id: '',
                    name: '',
                    image: '',
                    promotion_price: '',
                    unit_price: '',
                },
                pagination: {},
                checkOut: false,
                carts: [],
                cartAdd: {
                    id: '',
                    name: '',
                    image: '',
                    promotion_price: '',
                    unit_price: '',
                },
                badge: '0',
                qty: 1,
            }
        },
        mounted() {
            this.getProducts();
            this.viewCart();
        },
        computed: {
            getSubtotal() {
                return this.carts.reduce(
                    (a, b) => (b.promotion_price > 0) ? a + b.promotion_price * b.qty : a + b.unit_price * b.qty,
                    0
                )
            },
            getItemTotal() {
                return this.carts.reduce((total, item) => total + item.qty, 0)
            },
            changeValue(pro){

            }
        },
        methods: {
            getProducts(urlBase) {
                urlBase = urlBase || 'http://127.0.0.1:8000/api/products';
                axios.get(urlBase)
                    .then(res => {
                        this.products = res.data.data;
                        this.pagination = {
                            current_page: res.data.current_page,
                            last_page: res.data.last_page,
                            // next_page_url: res.data.next_page_url,
                            // prev_page_url: res.data.prev_page_url,
                            path_page: res.data.path,
                        };
                    })
                    .catch(err => console.log(err));
            },
            clickCallback(pageNum) {
                this.pagination.current_page = Number(pageNum);
                this.getProducts(this.pagination.path_page + '?page=' + this.pagination.current_page);
            },
            addCart(pro) {
                // this.cartAdd.id = pro.id;
                // this.cartAdd.name = pro.name;
                // this.cartAdd.promotion_price = pro.promotion_price;
                // this.cartAdd.unit_price = pro.unit_price;
                // this.cartAdd.image = pro.image;
                // this.carts.push(this.cartAdd);
                // this.cartAdd = {};
                const matchingProduct = this.carts.findIndex((item) => {
                    return item.id === pro.id;
                });
                if (matchingProduct > -1) {
                    let quantity = this.carts[matchingProduct].qty+=1;
                    localStorage.setItem('carts', JSON.stringify(quantity));
                } else {
                    pro.qty = 1;
                    this.carts.push(pro);
                }
                this.storeCart();
            },
            viewCart() {
                if (localStorage.getItem('carts')) {
                    this.carts = JSON.parse(localStorage.getItem('carts'));
                    this.badge = this.carts.length;
                }
            },
            removeCart(pro) {
                if (confirm("Do you really want to delete?")) {
                    this.carts.splice(pro, 1);
                    this.storeCart();
                }
            },
            clearAllCart() {
                this.carts = [];
                this.storeCart();
            },
            storeCart() {
                let parsed = JSON.stringify(this.carts);
                localStorage.setItem('carts', parsed);
                this.viewCart();
            }
        }
    }
</script>
<style lang="scss">
    .show {
        width: 100%;
        height: auto;
    }

    .fa {
        outline-style: none;
    }

    img {
        width: 250px;
        height: 250px;
    }

    .has_pro {
        text-decoration: line-through;
    }

    .fa-chevron-right, .fa-chevron-left {
        font-size: 30px;
        color: green;
    }

    .disabled {
        cursor: not-allowed;
    }

    .pagination {
        border: none;
    }
</style>
