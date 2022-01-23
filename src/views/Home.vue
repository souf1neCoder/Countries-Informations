<template>
  <div class="home">
    <div class="loader d-flex justify-content-center align-items-center" v-if="loader">
<div class="lds-hourglass"></div>
    </div>
      <aside class="side">
        <search />
      </aside>
      <section class="main">
        <welcome />
        <result />
        
        <Footer />
      
      </section>
      
  </div>
</template>

<script>

import search from '@/components/sidebar/search.vue';
import result from '@/components/main/result.vue';
import welcome from '@/components/main/welcome.vue';
import Footer from '@/components/main/Footer.vue';
import {ref} from 'vue';
export default {
  name: 'Home',

  components: {
    search,result,welcome,Footer
  },
  setup(){
    
    let loader = ref(true);
    function setTimeLoader(){
      setTimeout(()=>{
        loader.value = false;
      },5500)
    }
    setTimeLoader();
    return{
      loader
    }
  }
}
</script>
