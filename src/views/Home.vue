<template>
  <div class="home">
    <HeaderOnine/>
    <HeroOnine/>
    <WomenOnine/>
    <InstaOnine/>
    <PartnerOnine/>
    <FooterOnine/>
    
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import HeaderOnine from '@/components/HeaderOnine.vue'
import HeroOnine from '@/components/HeroOnine.vue'
import WomenOnine from '@/components/WomenOnine.vue'
import InstaOnine from '@/components/InstaOnine.vue'
import PartnerOnine from '@/components/PartnerOnine.vue'
import FooterOnine from '@/components/FooterOnine.vue'

export default {
  name: 'Home',
  components: {
    HeaderOnine,
    HeroOnine,
    WomenOnine,
    InstaOnine,
    PartnerOnine,
    FooterOnine
  }
}
</script>
