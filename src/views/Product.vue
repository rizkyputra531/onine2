<template>
<div class="product">
<HeaderOnine/>

<!-- Breadcrumb Section Begin -->
<div class="breacrumb-section text-left">
    <div class="container">
        <div class="row">
            <div class="col-lg-12">
                <div class="breadcrumb-text product-more">
                    <router-link to="/"><i class="fa fa-home"></i> Home</router-link>
                    <span>Detail</span>
                </div>
            </div>
        </div>
    </div>
</div>
<!-- Breadcrumb Section Begin -->

<!-- Product Shop Section Begin -->
<section class="product-shop spad page-details">
    <div class="container">
        <div class="row">
            <div class="col-lg-12">
                <div class="row">
                    <div class="col-lg-6">
                        <div class="product-pic-zoom">
                            <img class="product-big-img" :src="gambar_default" alt="" />
                        </div>
                        <div class="product-thumbs" v-if="productDetails.galleries.length > 0">
                            <carousel class="product-thumbs-track ps-slider carousel" :dots="true" :nav="false" :autoplay="true">
                                <div class="pt" v-for="ss in productDetails.galleries"
                                    :key="ss.id"
                                    @click="changeImage(ss.photo)" 
                                    :class="ss.photo == gambar_default ? 'active' : '' ">
                                    <img :src="ss.photo" alt="" />
                                </div>
                            </carousel>
                        </div>
                    </div>
                    <div class="col-lg-6">
                        <div class="product-details text-left">
                            <div class="pd-title">
                                <span>{{productDetails.type}}</span>
                                <h3>{{productDetails.name}}</h3>
                            </div>
                            <div class="pd-desc">
                                <p v-html="productDetails.description">
                                    
                                </p>
                                <h4>Rp. {{productDetails.price}}</h4>
                            </div>
                            <div class="quantity">
                                <router-link to="/cart">
                                <a @click="saveKeranjang(productDetails.id, productDetails.name, productDetails.price, productDetails.galleries[0].photo)"  href="#" class="primary-btn pd-cart">Add To Cart</a>
                                </router-link>
                            </div>
                        </div>
                     </div> 
                </div>
            </div>
        </div>
    </div>
</section>
<!-- Product Shop Section End -->

<RelatedOnine/>
<FooterOnine/>    
</div>
</template>

<script>

import HeaderOnine from '@/components/HeaderOnine.vue';
import FooterOnine from '@/components/FooterOnine.vue';
import RelatedOnine from '@/components/RelatedOnine.vue';
import carousel from 'vue-owl-carousel';
import axios from 'axios';

export default {
    name: "Product",
    components: {
        HeaderOnine,
        FooterOnine,
        carousel,
        RelatedOnine
    },
    data(){
        return{
            gambar_default:"",
            productDetails: [],
            keranjangUser:[]
        }
    },
    methods:{
        //mengganti gambar ketika di klik
        changeImage(urlImage) {
            this.gambar_default = urlImage;
        },
        setDataPicture(data) {
            // replace object productDetail dengan data dari API
            this.productDetails = data;
            // replace value gambar default dengan data dari API (galleries)
            this.gambar_default = data.galleries[0].photo; //varibale gambar_default diberi data foto dari API
        },
        saveKeranjang(idProduct, nameProduct, priceProduct, photoProduct){

            var productStored = { //penyimpanan sementara dari data API
                "id": idProduct,
                "name": nameProduct,
                "price": priceProduct,
                "photo": photoProduct
            }
            this.keranjangUser.push(productStored);
            const parsed = JSON.stringify(this.keranjangUser);
            localStorage.setItem('keranjangUser', parsed);
        }

    },
    mounted(){
        // Fungsi untuk melakukan localstorage dengan variable keranjangUser
        if (localStorage.getItem('keranjangUser')) {
            try {
                this.keranjangUser = JSON.parse(localStorage.getItem('keranjangUser'));
            } catch(e) {
                localStorage.removeItem('keranjangUser');
            }
        }

        axios
        .get("http://shayna-backend.belajarkoding.com/api/products", {
            params:{
                id: this.$route.params.id //mendapatkan API berdasarkan satu objek
            }
        })
        .then(res => (this.setDataPicture(res.data.data))) //mengambil API dengn function setDataPicture
        //eslint-disable-next-line no-console
        .catch(err => console.log(err));
 
    }
            
    
};
</script>

<style scoped>

.product-thumbs .pt{
  margin-right: 10px;
  height: 200px;
}

</style>

