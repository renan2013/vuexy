<template>
    <div id="demo-basic-card">
        <br>
        <div class="vx-row">
            <div class="vx-col w-full sm:w-1/2 lg:w-1/3 mb-base">
                <vx-card>
                    <div slot="no-body">
                        <img :src="card_1.img" alt="content-img" class="responsive card-img-top">
                    </div>
                    <h5 class="mb-2">{{ card_1.title }}</h5>
                    <p class="text-grey">{{ card_1.subtitle }}</p>
                    <p class="text-grey">{{ card_1.subtitle_2 }}</p>
                    <div class="flex justify-between flex-wrap">
                        <vs-button class="mt-4 mr-2 shadow-lg" type="gradient" color="#7367F0" gradient-color-secondary="#CE9FFC">Comprar</vs-button>
                        <vs-button class="mt-4" type="border" color="#b9b9b9">$20</vs-button>
                    </div>
                </vx-card>
            </div>

            <div class="vx-col w-full sm:w-1/2 lg:w-1/3 mb-base">
                <vx-card>
                    <div slot="no-body">
                    <img :src="card_2.img" alt="content-img" class="responsive card-img-top">
                    </div>
                    <h5 class="mb-2">{{ card_1.title }}</h5>
                    <p class="text-grey">{{ card_1.subtitle }}</p>
                    <p class="text-grey">{{ card_1.subtitle_2 }}</p>
                    <div class="flex justify-between flex-wrap">
                        <vs-button class="mt-4 mr-2 shadow-lg" type="gradient" color="#7367F0" gradient-color-secondary="#CE9FFC">Comprar</vs-button>
                        <vs-button class="mt-4" type="border" color="#b9b9b9">$40</vs-button>
                    </div>
                </vx-card>
            </div>

            <!-- CONTENT CARD - PROGRESS BAR/GOAL -->
            <div class="vx-col w-full sm:w-1/2 lg:w-1/3 mb-base">
                <vx-card>
                    <div slot="no-body">
                    <img :src="card_3.img" alt="content-img" class="responsive card-img-top">
                    </div>
                    <h5 class="mb-2">{{ card_1.title }}</h5>
                    <p class="text-grey">{{ card_1.subtitle }}</p>
                    <p class="text-grey">{{ card_1.subtitle_2 }}</p>
                    <div class="flex justify-between flex-wrap">
                        <vs-button class="mt-4 mr-2 shadow-lg" type="gradient" color="#7367F0" gradient-color-secondary="#CE9FFC">Comprar</vs-button>
                        <vs-button class="mt-4" type="border" color="#b9b9b9">$30</vs-button>
                    </div>
                </vx-card>
            </div>

        </div>

       
    </div>
</template>

<script>



export default{
  components: {
    
  },
  data () {
    return {
      // card 1
      card_1: {},
    

      chatLog: [],
      chatMsgInput: '',

    

      

      name  : '',
      email : '',
      msg   : '',

      playerOptions: {},
      settings: { // perfectscrollbar settings
        maxScrollbarLength: 60,
        wheelSpeed: .60
      }
    }
  },
  computed: {
    scrollbarTag () { return this.$store.getters.scrollbarTag }
  },
  mounted () {
    const scroll_el = this.$refs.chatLogPS.$el || this.$refs.chatLogPS
    scroll_el.scrollTop = this.$refs.chatLog.scrollHeight
  },
  created () {
    // Card 1
    this.$http.get('/api/users/pixinvent/product/1')
      .then((response) => { this.card_1 = response.data })
      .catch((error)   => { console.log(error) })

      // Card 2
    this.$http.get('/api/users/pixinvent/product/sales/1')
      .then((response) => { this.card_2 = response.data })
      .catch((error)   => { console.log(error) })

      // Card 3
    this.$http.get('/api/users/pixinvent/product/goals/1')
      .then((response) => { this.card_3 = response.data })
      .catch((error)   => { console.log(error) })

    

    
  }
}
</script>

<style lang="scss">
#demo-basic-card {
    .overlay-card {
        .vx-card__collapsible-content {
            max-height: 485px;
        }
    }

    .chat-card-log {
        height: 360px;

        .chat-sent-msg {
            background-color: #f2f4f7 !important;
        }
    }

    .card-video {
        .video-js {
            height: 370px;
        }
    }
}
</style>
