<template>
    <div id="profile-page">

        <!-- PROFILE HEADER -->
        <div class="profile-header">
            <div class="relative">
                <div class="cover-container rounded-t-lg">
                    <img :src="user_info.cover_img" alt="user-profile-cover" class="responsive block">
                </div>
                
            </div>
            
            <!-- <vx-navbar> -->
            <!-- </vx-navbar> -->
        </div>

        <!-- COL AREA -->
        <div class="vx-row">
            <!-- COL 1 -->
            <div class="vx-col w-full lg:w-1/4">
                <!-- ABOUT CARD -->
                <vx-card title="Quienes Somos" class="mt-base">
                    <!-- ACTION SLOT -->
                    <template slot="actions">
                        <feather-icon icon="MoreHorizontalIcon"></feather-icon>
                    </template>

                    <!-- USER BIO -->
                    <div class="user-bio">
                        <p>Somos una empresa visionaria de desarrollo de software a la medida de sus necesidades. Trabajamos en proyectos de investigación con las últimas tendencias en tecnologías emergentes.</p>
                    </div>

                    <!-- OTEHR DATA -->
                    <div class="mt-5">
                        <h6>Telefono:</h6>
                        <p>(506)2707-0477</p>
                    </div>

                    <div class="mt-5">
                        <h6>Dirección:</h6>
                        <p>Junquillo Arriba, a 100 mts del tanque del AyA, Puriscal, San José, Costa Rica</p>
                    </div>

                    <div class="mt-5">
                        <h6>Email:</h6>
                        <p>info@grupodivisoft.com</p>
                    </div>

                    <div class="mt-5">
                        <h6>Website:</h6>
                        <p>www.grupodivisoft.com</p>
                    </div>

                    <div class="social-links flex mt-4">
                        <feather-icon svgClasses="h-7 w-7 cursor-pointer bg-primary p-1 text-white rounded" class="mr-2" icon="FacebookIcon"></feather-icon>
                        <feather-icon svgClasses="h-7 w-7 cursor-pointer bg-primary p-1 text-white rounded" class="mr-2" icon="TwitterIcon"></feather-icon>
                     
                    </div>
                </vx-card>

               

               
            </div>

            <!-- COL 2 -->
            <div class="vx-col w-full lg:w-1/2">
                <vx-card class="mt-base" v-for="(post, index) in userPosts" :key="index">
                    <div>
                        <!-- POST HEADER -->
                        <div class="post-header flex justify-between mb-4">
                            <div class="flex items-center">
                                <div>
                                    <vs-avatar class="m-0" :src="userLatestPhotos[0]" size="45px"></vs-avatar>
                                </div>
                                <div class="ml-4">
                                    <h6>{{ post.author }}</h6>
                                    <small>{{ post.time}}</small>
                                    
                                </div>
                            </div>
                            
                        </div>

                        <!-- POST CONTENT -->
                      
                        <div class="post-media-container mb-6 mt-4">
                            <ul class="flex post-media-list">
                                <li class="post-media m-1 w-full" v-for="(media, mediaIdex) in post.media.slice(0, 2)" :key="mediaIdex">
                                    <img class="responsive rounded" :src="media.img" alt="user-upload" v-if="mediaType(media) == 'image'">
                                    <br>
                                    <div class="user-bio">{{ post.text }}</div>
                                </li>
                            </ul>
                            
                        </div>

                      
                    </div>
                </vx-card>
            </div>

            <!-- COL 3 -->
            <div class="vx-col w-full lg:w-1/4">

                <!-- LATEST PHOTOS -->
                <vx-card title="Equipo de Trabajo" class="mt-base">
                    <div class="vx-row pt-2">
                        <div class="vx-col w-1/2 sm:w-1/2 md:w-1/2 xl:1/4" v-for="(img, index) in userLatestPhotos" :key="index">
                            <img :src="img" alt="latest-upload" class="rounded mb-4 user-latest-image responsive">
                              
                        </div>
                        
                    </div>
                </vx-card>

             

               
            </div>
        </div>

        
    </div>
</template>

<script>
import { videoPlayer } from 'vue-video-player'
import 'video.js/dist/video-js.css'

export default {
  data () {
    return {
      isNavOpen: false,
      userPoll: '',
      user_info: {
        profile_img: require('@/assets/images/profile/user-uploads/user-13.jpg'),
        cover_img: require('@/assets/images/profile/user-uploads/desarrollo.jpg')
        
      },
      mediaExtensions: { img: ['jpg', 'jpeg', 'png', 'bmp', 'gif', 'exif', 'tiff'], video: ['avi', 'flv', 'wmv', 'mov', 'mp4', '3gp'] },
     //equipo de divisoft
      userLatestPhotos: [
        
        require('@/assets/images/profile/user-uploads/user-01.jpg'),
        require('@/assets/images/profile/user-uploads/user-02.jpg'),
        require('@/assets/images/profile/user-uploads/user-04.jpg')
     //fin de las fotos del equipo de divisoft

      ],
      
      userPosts: [
        {
          author     : 'Ademar Díaz Artavia',
          time       : 'Lunes 28 de Setiembre del 2020',
          isLiked    : true,
          text       : 'Creemos en la investigación y desarrollo de nuevos productos que ayuden a potenciar su trabajo empresarial y personal, evolucionando constantemente para tener las últimas tendencias en desarrollo de software de acuerdo a sus necesidades.',
          media      : [{ img: require('@/assets/images/profile/post-media/2.jpg') }],
          likes      : 145,
          comments   : 77,
          
          commentbox : '',
          
        }
        
        
      ],
     
      
      wasSidebarOpen: null
    }
  },
  computed: {
    mediaType () {
      return (media) => {
        if (media.img) {
          const ext = media.img.split('.').pop()
          if (this.mediaExtensions.img.includes(ext)) return 'image'
        } else if (media.sources && media.poster) {
          // other validations
          return 'video'
        }
      }
    },
    playerOptions () {
      return (media) => {
        return {
          height: '360',
          fluid: true,
          autoplay: false,
          muted: true,
          language: 'en',
          playbackRates: [0.7, 1.0, 1.5, 2.0],
          sources: media.sources,
          poster: media.poster
        }
      }
    }
  },
  methods: {
    loadContent () {
      this.$vs.loading({
        background: this.backgroundLoading,
        color: this.colorLoading,
        container: '#button-load-more-posts',
        scale: 0.45
      })
      setTimeout(() => {
        this.$vs.loading.close('#button-load-more-posts > .con-vs-loading')
      }, 3000)
    }
  },
  components: {
    videoPlayer
  },
  mounted () {
    this.wasSidebarOpen = this.$store.state.reduceButton
    this.$store.commit('TOGGLE_REDUCE_BUTTON', true)
  },
  beforeDestroy () {
    if (!this.wasSidebarOpen) this.$store.commit('TOGGLE_REDUCE_BUTTON', false)
  }
}

</script>


<style lang="scss">
@import "@/assets/scss/vuexy/pages/profile.scss";
</style>
