<!-- =========================================================================================
  File Name: DashboardAnalytics.vue
  Description: Dashboard Analytics
  ----------------------------------------------------------------------------------------
  Item Name: Vuexy - Vuejs, HTML & Laravel Admin Dashboard Template
  Author: Pixinvent
  Author URL: http://www.themeforest.net/user/pixinvent
========================================================================================== -->

<template>
      <div >
        
        <CarouselAutoplay />
        <CardBasic  />
        
      </div>

</template>

<script>

import CarouselAutoplay from '@/views/components/extra-components/carousel/CarouselAutoplay.vue'
import CardBasic from '@/views/ui-elements/card/CardBasic.vue'





export default {
  components: {

    CarouselAutoplay,
    CardBasic
   
   
   
  }
}
</script>

<style >
 
</style>
