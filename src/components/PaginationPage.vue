<template>
      <div class="pagination-block">
        <div v-if="this.def.spinnerSettings.spinner" class="loader">
          <div :class="loader()"></div>
        </div>
        <transition-group appear :css="animationPage() ? true : false" :name="animationPage()" mode="out-in">
          <div class="pagination-block__page"
               v-for="(item, index) in settings.array_data" v-if="item.active" :key="index"
               :class="[
                 def.pageSettings.pageClass
               ]"
          >
            <slot name="page" :originalEvent="item">
            </slot>
          </div>
        </transition-group>
      </div>
</template>
<script>
import { defaultsDeep } from 'lodash'
export default {
  name: 'PaginationPage',
  props: ['settings'],
  data: function () {
    return {
      defValues: {
        pageSettings: {
          pageClass: ''
        },
        spinnerSettings: {
          spinner: false,
          spinnerStyle: 'spinnerStyle-1',
          spinnerColor: '#fff'
        },
        animationSettings: {
          animationPage: ''
        }
      }
    }
  },
  computed: {
    def: function () {
      return defaultsDeep(this.settings.PaginationPageSettings, this.defValues)
    }
  },
  methods: {
    loader: function () {
      let spinnerStyle = ''
      switch (this.def.spinnerSettings.spinnerStyle) {
        case 'spinnerStyle-1':
          spinnerStyle = 'loader-1'
          break
        case 'spinnerStyle-2':
          spinnerStyle = 'loader-2'
          break
        default:
          spinnerStyle = 'loader-3'
      }
      return spinnerStyle
    },
    animationPage () {
      let animationPage = ''
      switch (this.def.animationSettings.animationPage) {
        case 'fade':
          animationPage = 'fade'
          break
        case 'slide':
          animationPage = 'slide'
          break
        case 'bounce':
          animationPage = 'bounce'
          break
      }
      return animationPage
    }
  },
  beforeMount () {
    let root = document.querySelector(':root')
    if (this.def.spinnerSettings.spinnerColor) {
      root.style.setProperty('--spinnerColor', this.def.spinnerSettings.spinnerColor)
    }
  }
}
</script>

<style lang="scss">
  .pagination-block {
    position: relative;
    height: 300px;
    font-size: 60px;
    text-align: center;
    color: #000;
    font-family: "Comic Sans MS", sans-serif;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  :root {
    --spinnerColor: #fff;
  }
  body {
    overflow: hidden;
  }
  .fade-enter-active {
    transition: opacity .3s ease;
  }

  .fade-enter, .fade-leave-to {
    opacity: 0;
    position: absolute;
  }

  .fade-enter-to, .fade-leave {
    opacity: 1;
  }
  .slide-enter {
    transform: translateX(100%);
  }
  .slide-enter-to {
    transform: translateX(0);
  }

  .slide-leave-active {
    position: absolute;
    opacity: 0;
  }

  .slide-leave {
    transform: translateX(0);
  }
  .slide-leave-to {
    transform: translateX(-100%);
  }

  .slide-enter-active,
  .slide-leave-active {
    transition: transform .3s ease-out;
  }
  .bounce-enter-active {
    animation: bounce-in .3s ease;

  }
  .bounce-leave-active {
    animation: bounce-in .3s reverse;
    position: absolute;
    opacity: 0;
  }
  @keyframes bounce-in {
    0% {
      transform: scale(0);
    }
    50% {
      transform: scale(1.1);
    }
    100% {
      transform: scale(1);
    }
  }
  .loader {
    width:100%;
    height: 100%;
    position: absolute;
    left: 0;
    top: 0;
    overflow: hidden;
    z-index: 1;

    &:before {
      content: '';
      background-color:rgba(0, 0, 0, .7);
      height:100%;
      position:absolute;
      width:100%;
      top:0;
      left:0;
    }
  }

  .loader-1,
  .loader-1:before,
  .loader-1:after {
    background: var(--spinnerColor);
    animation: load1 1s infinite ease-in-out;
    width: 1em;
    height: 4em;
  }

  .loader-1 {
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    color: var(--spinnerColor);
    text-indent: -9999em;
    position: absolute;
    font-size: 6px;
    animation-delay: -0.16s;
    z-index: 10;
  }

  .loader-1:before,
  .loader-1:after {
    position: absolute;
    top: 0;
    content: '';
  }

  .loader-1:before {
    left: -1.5em;
    animation-delay: -0.32s;
  }

  .loader-1:after {
    left: 1.5em;
  }

  @keyframes load1 {
    0%,
    80%,
    100% {
      box-shadow: 0 0;
      height: 4em;
    }
    40% {
      box-shadow: 0 -2em;
      height: 5em;
    }
  }

  .loader-2,
  .loader-2:before,
  .loader-2:after {
    border-radius: 50%;
    width: 2.5em;
    height: 2.5em;
    animation-fill-mode: both;
    animation: load7 1.8s infinite ease-in-out;
  }

  .loader-2 {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    color: var(--spinnerColor);
    font-size: 6px;
    text-indent: -9999em;
    animation-delay: -0.16s;
    z-index: 10;
  }

  .loader-2:before,
  .loader-2:after {
    content: '';
    position: absolute;
    top: 0;
  }

  .loader-2:before {
    left: -3.5em;
    animation-delay: -0.32s;
  }

  .loader-2:after {
    left: 3.5em;
  }
  @keyframes load7 {
    0%,
    80%,
    100% {
      box-shadow: 0 2.5em 0 -1.3em;
    }
    40% {
      box-shadow: 0 2.5em 0 0;

      @keyframes load2 {
        0% {
          transform: rotate(0deg);
        }
      }
    }
  }

  .loader-3 {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    color: var(--spinnerColor);
    font-size: 8px;
    width: 1em;
    height: 1em;
    border-radius: 50%;
    text-indent: -9999em;
    animation: load4 1.3s infinite linear;
    z-index: 1000;
  }

  @keyframes load4 {
    0%,
    100% {
      box-shadow: 0 -3em 0 0.2em, 2em -2em 0 0em, 3em 0 0 -1em, 2em 2em 0 -1em, 0 3em 0 -1em, -2em 2em 0 -1em, -3em 0 0 -1em, -2em -2em 0 0;
    }
    12.5% {
      box-shadow: 0 -3em 0 0, 2em -2em 0 0.2em, 3em 0 0 0, 2em 2em 0 -1em, 0 3em 0 -1em, -2em 2em 0 -1em, -3em 0 0 -1em, -2em -2em 0 -1em;
    }
    25% {
      box-shadow: 0 -3em 0 -0.5em, 2em -2em 0 0, 3em 0 0 0.2em, 2em 2em 0 0, 0 3em 0 -1em, -2em 2em 0 -1em, -3em 0 0 -1em, -2em -2em 0 -1em;
    }
    37.5% {
      box-shadow: 0 -3em 0 -1em, 2em -2em 0 -1em, 3em 0em 0 0, 2em 2em 0 0.2em, 0 3em 0 0em, -2em 2em 0 -1em, -3em 0em 0 -1em, -2em -2em 0 -1em;
    }
    50% {
      box-shadow: 0 -3em 0 -1em, 2em -2em 0 -1em, 3em 0 0 -1em, 2em 2em 0 0em, 0 3em 0 0.2em, -2em 2em 0 0, -3em 0em 0 -1em, -2em -2em 0 -1em;
    }
    62.5% {
      box-shadow: 0 -3em 0 -1em, 2em -2em 0 -1em, 3em 0 0 -1em, 2em 2em 0 -1em, 0 3em 0 0, -2em 2em 0 0.2em, -3em 0 0 0, -2em -2em 0 -1em;
    }
    75% {
      box-shadow: 0em -3em 0 -1em, 2em -2em 0 -1em, 3em 0em 0 -1em, 2em 2em 0 -1em, 0 3em 0 -1em, -2em 2em 0 0, -3em 0em 0 0.2em, -2em -2em 0 0;
    }
    87.5% {
      box-shadow: 0em -3em 0 0, 2em -2em 0 -1em, 3em 0 0 -1em, 2em 2em 0 -1em, 0 3em 0 -1em, -2em 2em 0 0, -3em 0em 0 0, -2em -2em 0 0.2em;
    }
  }
</style>
