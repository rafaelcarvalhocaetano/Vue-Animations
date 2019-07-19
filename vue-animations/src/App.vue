<template>
  <div id="app">
    <div class="jumbotron jumbotron-fluid">
      <div class="container">
        <h1 class="display-4">Animações</h1>
        <p class="lead">Criando animação com VUE</p>
      </div>
    </div>
    <!-- <div class="container">
      <button class="btn btn-primary mb-3" @click="mostrar = !mostrar">Alternar</button>
      <div class="alert alert-primary" v-if="!mostrar">Animação com vue 000/001</div>
      
      <transition name="fade">
        <div class="alert alert-primary" v-if="mostrar">Animação com vue 000/002</div>
      </transition> 
      <transition name="zoom">
        <div class="alert alert-primary" v-if="mostrar">Animação com vue 000/002</div>
      </transition> 
      <transition name="slide" type="animation" :duration="{ enter: 1200, leave: 500}">
        <div class="alert alert-primary" v-if="mostrar">Animação com vue 000/002</div>
      </transition> 
      <transition
        enter-class=""
        enter-active-class="animated bounceInLeft"
        enter-to-class=""

        leave-class=""
        leave-active-class="animated bounceOutDown" >
        <div class="alert alert-primary" v-if="mostrar">Animação com vue 000/002</div>
      </transition>
      
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
        :css="false">
        
      <transition
        appear
        appear-class=""
        appear-active-class="animated flipInY"
        appear-to-class=""

        @before-appear="beforeAppear"
        @appear="appear"
        @after-appear="afterAppear"
        @appear-cancelled="canceledAppear"

        enter-class=""
        enter-active-class="animated bounceInLeft"
        enter-to-class=""

        leave-class=""
        leave-active-class="animated bounceOutLeft"
        leave-to-class="">

        <div class="alert alert-primary" v-if="mostrar">Animação com vue 000/002</div>
      </transition> 
      <div class="form-group">
        <label>Animação:</label>
        <select class="form-control" v-model="animacaoSelecionada">
          <option value="fade">Fade</option>
          <option value="zoom">Zoom</option>
          <option value="slide">Slide</option>
        </select>
      </div>

      <div class="form-group">
      <label>Mensagens:</label>
      <select class="form-control" v-model="alertaAtual">
        <option value="primary">Primary</option>
        <option value="success">Success</option>
        <option value="danger">Danger</option>
      </select>
      </div>


      <div class="form-group">
      <label>Mensagens:</label>
      <select class="form-control" v-model="alertaAtual">
        <option value="AppHome">Home</option>
        <option value="AppSobre">Sobre</option>
      </select>
      </div>

      <transition :name="animacaoSelecionada" mode="out-in">
        <div class="alert alert-primary" v-if="alertaAtual === 'primary'" key="primary">Initialize primary</div>
        <div class="alert alert-success" v-if="alertaAtual === 'success'" key="success">Initialize success</div>
        <div class="alert alert-danger" v-if="alertaAtual === 'danger'"   key="danger">Initialize danger</div>
        <div :class="classeDeAlerta" :key="alertaAtual">Initialize {{ alertaAtual }}</div>
        <component :is="componentSelecionado">
        </component>
      </transition>
    </div> -->

    <div class="container">
      <h3 class="font-weight-light">Tecnologias</h3>

      <div class="row">

        <div class="col-sm-2">
          <button class="btn btn-info" @click="embaralhar">Embaralhar</button>
        </div>

        <!-- INPUT -->
        <div class="col-sm-10">
          <div class="form-group">
            <input type="text" 
              class="form-control"
              placeholder="Insira um novo item e pressione Enter"
              @keyup.enter="adicionar"
              ref="input">
          </div>
        </div>
      </div>

      <transition-group tag="ul" class="list-group" name="list">
        <li class="list-group-item" 
          v-for="(tec, i) in tecnologias" :key="tec">
          <span>{{ tec }}</span>
          <button 
            class="btn btn-danger btn-sm float-right"
            @click="remover(i)"
            > X </button>
        </li>
      </transition-group>

    </div>
  </div>
</template>

<script>

import { clearInterval } from 'timers';
import { shuffle } from 'lodash';


export default {
  data() {
    return {
      tecnologias: ['JavaScript', 'Vue', 'Vuex', 'Vue Router']
    }
  },
  methods: {
    adicionar(event) {
      const novoItem = event.target.value;
      if (novoItem) {
        const indice = Math.floor(Math.random() * this.tecnologias.length);
        this.tecnologias.splice(indice, 0, novoItem);
        this.$refs.input.value = '';
      }
    },
    remover(indice) {
      this.tecnologias.splice(indice, 1);
    },
    embaralhar(e) {
      this.tecnologias = shuffle(this.tecnologias);
    }

  }
  // components: {
  //   AppHome: () => import('./component/Home'),
  //   AppSobre: () => import('./component/Sobre')
  // },
  // data() {
  //   return {
  //     mostrar: false,
  //     animacaoSelecionada: 'fade',
  //     alertaAtual: 'info',
  //     componentSelecionado: 'AppHome'
  //   }
  // },
  // computed: {
  //   classeDeAlerta() {
  //     return {
  //       alert: true,
  //       [`alert-${this.alertaAtual}`]: true
  //     }
  //   }
  // }
  // methods: {
    // beforeEnter(el) {
    //   el.style.opacity = 0;
    // },4
    // enter(el, done) {
    //   let count = 0;
    //   const interval = setInterval(() => {
    //     el.style.opacity = Number(el.style.opacity) + 0.1;
    //     count ++;

    //     if (count > 10) {
    //       clearInterval(interval);
    //       done();
    //     }        
    //   }, 300);
    // },
    // afterEnter(el) {},
    // enterCancelled(el) {},
    // beforeLeave(el) {
    //   el.style.transition = 'width 0.5s';
    //   el.style.overflow = 'hidden';
    //   el.style.whiteSpace = 'nowrap';
    // },
    // leave(el, done) {
    //   let count = 0;
    //   const tamanho = el.offsetWidth;
    //   const interval = setInterval(() => {
    //     el.style.width = (tamanho * (1 - (count / 10))) + 'px';
    //     count ++;

    //     if (count > 10) {
    //       clearInterval(interval);
    //       done();
    //     }
    //   },  300);
    // },
    // afterLeave(el) {},
    // leaveCancelled(el) {},
    // appear
  //   beforeAppear(el) {
  //     console.log(' ap 001 ', el);
  //   },
  //   appear(el, done) {
  //     console.log(' ap 002 ', el);
  //   },
  //   afterAppear(el) {
  //     console.log(' ap 003 ', el);
  //   },
  //   canceledAppear(el) {
  //     console.log(' ap 004 ', el);
  //   }
  // } 
}
</script>

<style scoped>
  /* body {
    width: 100vw;
    height: 100vh;
    overflow: hidden;
  } */

  .list-enter, .list-leave-to {
    opacity: 0;
    transform: translateX(-70px);
  }

  .list-enter-active, .list-leave-active, .list-move {
    transition: all 1s;
  }

  .list-leave-active {
    position: absolute;
    width: calc(100% - 100px);
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

/************* 003 - transition *************/
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
  transition: opacity 0.7s;

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