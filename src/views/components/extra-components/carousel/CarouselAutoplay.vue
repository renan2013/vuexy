<!-- =========================================================================================
    File Name: CarouselAutplay.vue
    Description: Carousel with Autplay
    ----------------------------------------------------------------------------------------
    Item Name: Vuexy - Vuejs, HTML & Laravel Admin Dashboard Template
      Author: Pixinvent
    Author URL: http://www.themeforest.net/user/pixinvent
========================================================================================== -->


<template>
    <div  >
          <!-- swiper -->
          <swiper :options="swiperOption" :dir="$vs.rtl ? 'rtl' : 'ltr'" :key="$vs.rtl">
            <swiper-slide>
              <img class="responsive" src="https://linuxpathshala.com/wp-content/uploads/2018/02/Anroid-Ios.jpg" alt="banner">
            </swiper-slide>
            <swiper-slide>
              <img class="responsive" src="https://miro.medium.com/max/1200/1*HouiY8Hgtw8YRtnj680epw.png" alt="banner">
            </swiper-slide>
            <swiper-slide>
              <img class="responsive" src="https://invoiceoffice.com/wp-content/uploads/2017/01/home_wallet_blog1-1200x800-1200x480.jpg" alt="banner">
            </swiper-slide>
          
            <div class="swiper-pagination" slot="pagination"></div>
            <div class="swiper-button-prev swiper-button-white" slot="button-prev"></div>
            <div class="swiper-button-next swiper-button-white" slot="button-next"></div>
          </swiper>

          
      </div>
</template>

<script>
import 'swiper/dist/css/swiper.min.css'
import { swiper, swiperSlide } from 'vue-awesome-swiper'

export default {
  data () {
    return {
      swiperOption: {
        spaceBetween: 30,
        centeredSlides: true,
        autoplay: {
          delay: 2500,
          disableOnInteraction: false
        },
        pagination: {
          el: '.swiper-pagination',
          clickable: true
        },
        navigation: {
          nextEl: '.swiper-button-next',
          prevEl: '.swiper-button-prev'
        }
      }
    }
  },
  components: {
    swiper,
    swiperSlide
  }
}
</script>
