<template>
  <div id="app">
    <div class="jumbotron jumbotron-fluid">
      <div class="container">
        <h1 class="display-4">Animações</h1>
        <p class="lead">Criando animação com VUE</p>
      </div>
    </div>
    <div class="container">
      <button class="btn btn-primary mb-3" @click="mostrar = !mostrar">Alternar</button>
      <!-- <div class="alert alert-primary" v-if="!mostrar">Animação com vue 000/001</div> -->

      <!-- <transition name="fade">
        <div class="alert alert-primary" v-if="mostrar">Animação com vue 000/002</div>
      </transition> 
      <transition name="zoom">
        <div class="alert alert-primary" v-if="mostrar">Animação com vue 000/002</div>
      </transition> -->

      <!-- <transition name="slide" type="animation" :duration="{ enter: 1200, leave: 500}">
        <div class="alert alert-primary" v-if="mostrar">Animação com vue 000/002</div>
      </transition> -->

      <!-- <transition
        enter-class=""
        enter-active-class="animated bounceInLeft"
        enter-to-class=""

        leave-class=""
        leave-active-class="animated bounceOutDown"
      >
        <div class="alert alert-primary" v-if="mostrar">Animação com vue 000/002</div>
      </transition> -->

       <transition
        appear

        @before-enter="beforeEnter"
        @enter="enter"
        @after-enter="afterEnter"
        @enter-cancelled="enterCancelled"

        @before-leave="beforeLeave"
        @leave="leave"
        @after-leave="afterLeave"
        @leave-cancelled="leaveCancelled"

        :css="false"
        >
        <div class="alert alert-primary" v-if="mostrar">Animação com vue 000/002</div>
      </transition>
    </div>
  </div>
</template>

<script>
import { clearInterval } from 'timers';
export default {
  data() {
    return {
      mostrar: false
    }
  },
  methods: {
    beforeEnter(el) {
      el.style.opacity = 0;
    },
    enter(el, done) {
      let count = 0;
      const interval = setInterval(() => {
        el.style.opacity = Number(el.style.opacity) + 0.1;
        count ++;

        if (count > 10) {
          clearInterval(interval);
          done();
        }        
      }, 300);
    },
    afterEnter(el) {
    },
    enterCancelled(el) {

    },
    beforeLeave(el) {
      el.style.transition = 'width 0.5s';
      el.style.overflow = 'hidden';
      el.style.whiteSpace = 'nowrap';
    },
    leave(el, done) {
      let count = 0;
      const tamanho = el.offsetWidth;
      const interval = setInterval(() => {
        el.style.width = (tamanho * (1 - (count / 10))) + 'px';
        count ++;

        if (count > 10) {
          clearInterval(interval);
          done();
        }
      },  300);
    },
    afterLeave(el) {

    },
    leaveCancelled(el) {
    }
  } 
}
</script>

<style>
  body {
    width: 100vw;
    height: 100vh;
    overflow: hidden;
  }
</style>


<style scoped>

.slide-enter {
  opacity: 0;
}
.slide-enter-active {
  animation: slide 0.7s cubic-bezier(.87, .36, 1, .23);
  transition: opacity 0.7s cubic-bezier(.87, .36, 1, .23);
}
.slide-enter-to {
  opacity: 1;
}
.slide-leave {
  opacity: 1;
}
.slide-leave-active {
  animation: slide 0.7s reverse;
  /* animation: slide-out 0.7s; */
  transition: opacity 2s;

}
.slide-leave-to {
  opacity: 0;
}

@keyframes slide {
  /* from {}
  to {}
  || */

  0% {
    transform: translatex(-100px);
  }
  100% {
    transform: translatex(0px);
  }
}
@keyframes slide-out {
  0% {
    transform: translatex(0px);
  }
  100% {
    transform: translatex(-100px);
  }
}
</style>

/ ******************** 001  FADE ****************** /
/* entrada */
.fade-enter, .fade-leave-to {
  opacity: 0;
}
/* como ficará no click */
.fade-enter-active, .fade-leave-active {
  transition: opacity 1s;
}
/* estado final da animação*/
/** por padrão o transition já usa o por início e fim a opacidade em 1% **/
.fade-enter-to, .fade-leave {
  opacity: 1;
}

/****************** SAíDA ******************/
.fade-leave {
  opacity: 1;
}
.fade-leave-active {
  transition: opacity 1s;
}
.fade-leave-to {
  opacity: 0;
}

/*************** 002 - ZOOM **************/

.zoom-enter {
  transform: scale(0);
}
.zoom-enter-active {
  transition: transform 0.5s;
}
.zoom-enter-to {
  transform: scale(1);
}
.zoom-leave {
  transform: scale(1);
}
.zoom-leave-active {
  transition: transform 0.5s;
}
.zoom-leave-to {
  transform: scale(0);
}