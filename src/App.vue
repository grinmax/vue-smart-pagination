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
    <pagination-control :settings="settings" @callMethod="test"/>
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
          data: 'apple'
        },
        {
          data: 'banana'
        },
        {
          data: 'orange'
        }
      ]
    }
  },
  methods: {
    test: function (e) {
      console.log(e)
    }
  },
  computed: {
    settings: function () {
      return {
        array_data: this.array_data,
        PaginationControlSettings: {
          buttonsSettings: {
            maxButtons: 6
          },
          arrowsSettings: {
            hideArrows: false,
            arrowStyle: 'styleArrow-1'
          }
        },
        PaginationPageSettings: {
          spinnerSettings: {
            spinner: true,
            spinnerStyle: 'spinnerStyle-3'
          },
          animationSettings: {
            animationPage: 'bounce'
          }
        }
      }
    }
  }
}
</script>
