<template>
  <main>
    <div>
      <h1 class="titreProduit">Produit</h1>
      <div class="positionSwiper">
        <swiper ref="mySwiper" :navigation="true" :thumbs="{ swiper: thumbsSwiper }" :modules="modules" class="mySwiper"
           :loop="true" :breakpoints="{
            '320': {
              slidesPerView: 1,
            },
            '570': {
              slidesPerView: 1,
            },
            '768': {
              slidesPerView: 1,
            },

            '992': {
              slidesPerView: 1,
            },
            '1024': {
              slidesPerView: 1,
            },
            '1200': {
              slidesPerView: 1,
            },
          }">
          <swiper-slide v-for="m in montres" :key="m.id">
            <Montre class="swiper-slide" :montre="m" @AddMOntre="AddMOntre" />
          </swiper-slide>

          <span class="imgCadran">
            <img src="/image/cadran.png" />
          </span>
        </swiper>
      </div>

      <h2 class="choixBracelet">Choisissez la couleur de votre bracelet :</h2>

      <!--
      <div class="alignPastilleCouleur">
        <div class="pastillas" :class="{ selectedPastillas: p.id === selectedPastillas}" 
          :style="p"
          v-for="p in pastille"
          :key="p.id"
          @click="selected(p.id)"
          ></div>
      </div>
      -->
    </div>
    <div>
      <swiper :spaceBetween="3" :slidesPerView="7" :freeMode="true" 
        :watchSlidesProgress="true" :modules="modules" class="swiperPastille">
        <swiper-slide class="alignPastilleCouleur" v-for="(element , position) in montres" @click="setThumbsSwiper(position)" :key="element.id">
          <div class="pastillas" :style="{ backgroundColor: element.pasti }"></div>
        </swiper-slide>
      </swiper>
    </div>

    <h2>Caractèristique du bracelet: Yellow Pastel</h2>
  </main>
</template>

<script>
import Montre from "@/components/Montre.vue";
import { Navigation, Pagination, Scrollbar, FreeMode, Thumbs } from "swiper";
import { Swiper, SwiperSlide } from "swiper/vue";

// Import Swiper styles
import "swiper/css";
import "swiper/css/navigation";
import "swiper/css/pagination";
import "swiper/css/scrollbar";
import "swiper/css/thumbs";
import "swiper/css/free-mode";

import SwiperCore from "swiper/core";
SwiperCore.use([Navigation, Thumbs]);


export default {
  name: "ProductComponent",
  components: { Montre, Swiper, SwiperSlide },
  // mounted () {
  //   window.$s = this.$refs.mySwiper
  //   console.log ('on mounted > !' , this.$refs.mySwiper.swiper)
  // },
  data () {
    return {
      selectedPastillas: undefined,
      selected: undefined,
      montres:  require('../data/montreData.json'),
    };
  },
  setup() {
    const onSwiper = (swiper) => {
      console.log(swiper);
    };
    const onSlideChange = () => {
      console.log("slide change");
    };

    return {
      onSwiper,
      onSlideChange,
      modules: [Navigation, Pagination, Scrollbar, FreeMode, Thumbs],
    };
  },
  methods: {
    setThumbsSwiper(element) {
      console.log('jai lance la commande pour changer le slider', element);
      this.$refs.mySwiper.$el.swiper.slideToLoop(element, 2000);
      if(this.breakpoints.slidesPerView > 1) {
        element+1
        console.log('if breakpoint');
      }
     
      //this.thumbsSwiper = swiper;
      //console.log(this.thumbsSwiper);
    },
    AddMOntre(montre) {
      this.montres.push(montre);
    },
  },
};
</script>

<style scoped>
/*
.grid {
  display: flex;
  justify-content: space-evenly;
  width: 80%;
  margin: 50px auto;

}
*/
.imgCadran  {
 width:100%;
 height:100%;
}

img { 
  position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 200;
    width:500px;
}
.swiper-button-prev, .swiper-rtl .swiper-button-next {
    left: 10px;
    right: auto;
    z-index: 300;
}
.alignPastilleCouleur {
  display: flex;
  justify-content: space-evenly;
  margin: 30px 0 30px 0;
}

ul {
  list-style: none;
  text-decoration: none;
}

.pastillas {
  height: 45px;
  width: 45px;
  border-radius: 50%;
  cursor: pointer;
  box-shadow: 3px 3px 5px 0 rgba(0, 0, 0, 0.75);
}

.positionSwiper {
  align-items: center;
}

.swiper-slide {
  align-items: center;
  display: -webkit-box;
  display: -ms-flexbox;
  display: -webkit-flex;
  display: flex;
  -webkit-box-pack: center;
  -ms-flex-pack: center;
  -webkit-justify-content: center;
  justify-content: center;
  -webkit-box-align: center;
  -ms-flex-align: center;
  -webkit-align-items: center;
}

h1,
h2 {
  margin-left: 45px;
}
</style>
