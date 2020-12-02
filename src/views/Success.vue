<template>
<div class="success">
        <div class="d-flex success-checkout align-items-center justify-content-center">
        <div class="col col-lg-4 text-center">
            <img src="img/success-buy.png" alt="" width="294">
            <h3 class="mt-4">
                Konfirmasi Pembayaran!
            </h3>
            <p class="mt-2">
                Silakan konfirmasi pembayaran melalui link berikut  <br/> <a class="" href="https://linktr.ee/sobatonine" >Sobat Onine</a>
            </p>
            <p>
            <router-link to="/" @click="removeItem()" class="primary-btn pd-cart mt-3">Back to Home</router-link>
            </p>
        </div>
    </div>
    </div>
</template>

<script>

export default {
    name: "Succes",
    
    data () {
        return {
        // keranjangUserStorage: localStorage.getItem('keranjangUser')

        };
    },

    methods : {
        // removeItem: function(){
        //     localStorage.removeItem('keranjangUser');
        //     this.keranjangUserStorage = localStorage.getItem('keranjangUser');
        //     window.location.reload();

        // }
        removeItem(){

            // cari tau id dari item yg akan dihapus
            let keranjangUserStorage = JSON.parse(localStorage.getItem("keranjangUser"));
           
            this.keranjangUser.splice(keranjangUserStorage);

            
            const parsed = JSON.stringify(this.keranjangUser);
            localStorage.setItem('keranjangUser', parsed);
            window.location.reload();

            
        }

    },
    mounted() {
        if (localStorage.getItem('keranjangUser')) { //validasi localstorage, jika ada maka lanjut, jika tidak ada maka stop
            try {
                this.keranjangUser = JSON.parse(localStorage.getItem('keranjangUser'));
            } catch(e) {
                localStorage.removeItem('keranjangUser');
            }
            }
        // // Clear the browser cache data in localStorage when closing the browser window
        //     window.onbeforeunload = function (e) {
        //         var storage = window.localStorage;
        //         storage.clear()
        //     }
    }
};
</script>

<style scoped>
a:link {
color:#3333FF;
}
a:hover {
color:#000066;
}
a:visited {
/* color:#663366; */
}
</style>