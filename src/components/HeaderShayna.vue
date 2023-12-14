<template>
    <!-- Header Section Begin -->
    <header class="header-section">
        <div class="header-top">
            <div class="container">
                <div class="ht-left">
                    <div class="mail-service">
                        <i class=" fa fa-envelope"></i> loveshop@gmail.com
                    </div>
                    <div class="phone-service">
                        <i class=" fa fa-phone"></i> +628 22081996
                    </div>
                </div>
            </div>
        </div>
        <div class="container">
            <div class="inner-header">
                <div class="row">
                    <div class="col-lg-2 col-md-2">
                        <div class="logo">
                            <a href="/">
                                <h4>Love<strong>Shop</strong></h4>
                            </a>
                        </div>
                    </div>
                    <div class="col-lg-6 col-md-6"></div>
                    <div class="col-lg-3 text-right col-md-3">
                        <ul class="nav-right gap-2">
                            <li class="cart-icon">
                                Cart &nbsp;
                                <a href="#">
                                    <i class="icon_bag_alt"></i>
                                    <span>{{  keranjangUser.length }}</span>
                                </a>
                                <div class="cart-hover">
                                    <div class="select-items">
                                        <table>
                                            <tbody v-if="keranjangUser.length > 0">
                                                <tr v-for="keranjang in keranjangUser" :key="keranjang.id">
                                                    <td class="si-pic">
                                                        <img class="photo-item" :src="keranjang.photo" alt="" />
                                                    </td>
                                                    <td class="si-text">
                                                        <div class="product-selected">
                                                            <p>{{ keranjang.price }} x 1</p>
                                                            <h6>{{ keranjang.name }}</h6>
                                                        </div>
                                                    </td>
                                                    <td @click="removeItem(keranjang.id)" class="si-close">
                                                        <i class="ti-close"></i>
                                                    </td>
                                                </tr>
                                            </tbody>
                                            <tbody v-else>
                                                <tr>
                                                    <td>Keranjang Kosong</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                    </div>
                                    <div class="select-total">
                                        <span>total:</span>
                                        <h5>Rp. {{ totalHarga }}</h5>
                                    </div>
                                    <div class="select-button">
                                        <router-link to="cart" class="primary-btn view-card">VIEW CARD</router-link>
                                        <a href="#" class="primary-btn checkout-btn">CHECK OUT</a>
                                    </div>
                                </div>
                            </li>
                            <li class="nav-item rounded ">
                                <a href="#" class="primary-btn login-card">Sign In</a>
                            </li>
                        </ul>
                    </div>
                </div>


            </div>
        </div>
    </header>
    <!-- Header End -->
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

export default {
    name: 'HeaderShayna',
    data() {
        return {
            keranjangUser: []
        };
    },
    methods: {
        removeItem(idx) {
            // cari tahu id dari si item yang dihapus
            let keranjangUserStorage = JSON.parse(localStorage.getItem('keranjangUser'));
            let itemKeranjangUserStorage = keranjangUserStorage.map(itemKeranjangUserStorage => itemKeranjangUserStorage.id);

            // cocok idx item dengan id yang ada di storage
            let index = itemKeranjangUserStorage.findIndex(id => id == idx);
            this.keranjangUser.splice(index, 1);

            const parsed = JSON.stringify(this.keranjangUser);
            localStorage.setItem('keranjangUser', parsed);
            window.location.reload();

        }
    },
    mounted() {
        if (localStorage.getItem('keranjangUser')) {
            try {
                this.keranjangUser = JSON.parse(localStorage.getItem('keranjangUser'));
            } catch (e) {
                localStorage.removeItem('keranjangUser');
            }
        }
    },
    computed: {
        totalHarga() {
            return this.keranjangUser.reduce(function(items, data) {
                return items + data.price;
            }, 0);
        }
    }
}
</script>

<style scoped>
.cart-icon {
    margin-right: 30px;
}

.photo-item {
    width : 80px;
    height : 80px;
}
</style>