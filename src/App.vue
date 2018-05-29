<template>
  <div id="app">
    <pagination-page :settings="settings">
      <div slot="page" slot-scope="item">
        <template v-if="item.originalEvent.components != undefined">
          <components :is="item.originalEvent.components"></components>
        </template>
        <template v-else>
          <div >{{item.originalEvent.data}}</div>
        </template>
      </div>
    </pagination-page>
    <pagination-control :settings="settings"/>
    <div class="testing">
      <div class="arrows">
        <button @click="arrowView1()">Вид стрелок 1</button>
        <button @click="arrowView2()">Вид стрелок 2</button>
        <button @click="arrowView3()">Вид стрелок 3</button>
        <button @click="arrowShow()">Показать стрелки</button>
        <button @click="arrowHide()">Скрыть стрелки</button>
      </div>
      <div class="buttons">
        <button @click="maxButtons3()">Количество кнопок 3</button>
        <button @click="maxButtons5()">Количество кнопок 5</button>
        <button @click="buttonsStyle1()">Вид кнопок 1</button>
        <button @click="buttonsStyle2()">Вид кнопок 2</button>
      </div>
      <div class="spinner">
        <button @click="spinnerShow()">Показать спиннер</button>
        <button @click="spinnerHide()">Скрыть спиннер</button>
        <button @click="spinnerStyles1()">Вид спиннера 1</button>
        <button @click="spinnerStyles2()">Вид спиннера 2</button>
        <button @click="spinnerStyles3()">Вид спиннера 3</button>
      </div>
      <div class="animation">
        <button @click="animationView1()">Вид анимации 1</button>
        <button @click="animationView2()">Вид анимации 2</button>
        <button @click="animationView3()">Вид анимации 3</button>
        <button @click="animationNo()">Без анимации</button>
      </div>
    </div>
  </div>
</template>

<script>
import PaginationPage from './components/PaginationPage'
import PaginationControl from './components/PaginationControl'
import test1 from './components/test1.vue'
import test2 from './components/test2.vue'
import test3 from './components/test3.vue'

export default {
  name: 'App',
  components: {
    PaginationPage,
    PaginationControl,
    test1,
    test2,
    test3
  },
  data: function () {
    return {
      settingsDefault: {
        array_data: [
          {
            data: 'apple',
            components: 'test1'
          },
          {
            data: 'banana',
            components: 'test2'
          },
          {
            data: 'orange',
            components: 'test3'
          },
          {
            data: 'Page 4'
          },
          {
            data: 'Page 5'
          },
          {
            data: 'Page 6'
          }
        ],
        PaginationControlSettings: {
          buttonsSettings: {
            maxButtons: 5,
            allPageButtonsStyle: {
              'background': '',
              'borderColor': '',
              'color': '',
              'backgroundHover': '',
              'borderColorHover': '',
              'colorHover': '',
              'fontFamily': ''
            },
            currentPageButtonStyle: {
              'backgroundActive': '',
              'borderColorActive': '',
              'colorActive': ''
            }
          },
          arrowsSettings: {
            hideArrows: false,
            arrowStyle: 'styleArrow-1'
          }
        },
        PaginationPageSettings: {
          spinnerSettings: {
            spinner: false,
            spinnerStyle: 'spinnerStyle-3'
          },
          animationSettings: {
            animationPage: 'bounce'
          }
        }
      }
    }
  },
  methods: {
    arrowView1: function (e) {
      this.settings.PaginationControlSettings.arrowsSettings.arrowStyle = 'styleArrow-1'
    },
    arrowView2: function (e) {
      this.settings.PaginationControlSettings.arrowsSettings.arrowStyle = 'styleArrow-2'
    },
    arrowView3: function (e) {
      this.settings.PaginationControlSettings.arrowsSettings.arrowStyle = 'styleArrow-3'
    },
    maxButtons3: function (e) {
      this.settings.PaginationControlSettings.buttonsSettings.maxButtons = 3
    },
    maxButtons5: function (e) {
      this.settings.PaginationControlSettings.buttonsSettings.maxButtons = 5
    },
    buttonsStyle1: function (e) {
      this.settings.PaginationControlSettings.buttonsSettings.allPageButtonsStyle.background = '#000'
      this.settings.PaginationControlSettings.buttonsSettings.allPageButtonsStyle.borderColor = '#000'
    },
    buttonsStyle2: function (e) {
      this.settings.PaginationControlSettings.buttonsSettings.allPageButtonsStyle.background = 'Tomato'
      this.settings.PaginationControlSettings.buttonsSettings.allPageButtonsStyle.borderColor = 'Tomato'
      this.settings.PaginationControlSettings.buttonsSettings.allPageButtonsStyle.color = '#fff'
    },
    arrowShow: function (e) {
      this.settings.PaginationControlSettings.arrowsSettings.hideArrows = false
    },
    arrowHide: function (e) {
      this.settings.PaginationControlSettings.arrowsSettings.hideArrows = true
    },
    spinnerShow: function (e) {
      this.settings.PaginationPageSettings.spinnerSettings.spinner = true
    },
    spinnerHide: function (e) {
      this.settings.PaginationPageSettings.spinnerSettings.spinner = false
    },
    spinnerStyles1: function (e) {
      this.settings.PaginationPageSettings.spinnerSettings.spinnerStyle = 'spinnerStyle-1'
    },
    spinnerStyles2: function (e) {
      this.settings.PaginationPageSettings.spinnerSettings.spinnerStyle = 'spinnerStyle-2'
    },
    spinnerStyles3: function (e) {
      this.settings.PaginationPageSettings.spinnerSettings.spinnerStyle = 'spinnerStyle-3'
    },
    animationView1: function (e) {
      this.settings.PaginationPageSettings.animationSettings.animationPage = 'fade'
    },
    animationView2: function (e) {
      this.settings.PaginationPageSettings.animationSettings.animationPage = 'slide'
    },
    animationView3: function (e) {
      this.settings.PaginationPageSettings.animationSettings.animationPage = 'bounce'
    },
    animationNo: function (e) {
      this.settings.PaginationPageSettings.animationSettings.animationPage = 'default'
    }
  },
  computed: {
    settings: {
      get: function () {
        return this.settingsDefault
      },
      set: function (data) {
        this.settingsDefault = data
      }
    }
  }
}
</script>

<style>
  .testing {
    margin-top: 50px;
    display: flex;
    justify-content: center;
  }
  .testing button {
    width: 150px;
    height: 30px;
    line-height: 30px;
    border-radius: 10px;
    background: #fff;
    color: #02C8F3;
    border: 1px solid #02C8F3;
    cursor: pointer;
    margin-bottom: 10px;
  }
  .arrows, .buttons, .spinner, .animation {
    display: flex;
    flex-direction: column;
    margin: 0 10px;
  }
</style>
