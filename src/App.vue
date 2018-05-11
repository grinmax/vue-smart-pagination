<template>
  <div id="app">
    <pagination-page :settings="settings" />
    <pagination-control :settings="settings" @callMethod="test"/>
  </div>
</template>

<script>
import PaginationPage from './components/PaginationPage'
import PaginationControl from './components/PaginationControl'

export default {
  name: 'App',
  components: {
    PaginationPage,
    PaginationControl
  },
  data: function () {
    return {
      pages: [
        {
          content: 'Page № 1'
        },
        {
          content: 'Page № 2'
        },
        {
          content: 'Page № 3'
        },
        {
          content: 'Page № 4'
        },
        {
          content: 'Page № 5'
        },
        {
          content: 'Page № 6'
        },
        {
          content: 'Page № 7'
        },
        {
          content: 'Page № 8'
        },
        {
          content: 'Page № 9'
        },
        {
          content: 'Page № 10'
        },
        {
          content: 'Page № 11'
        },
        {
          content: 'Page № 12'
        },
        {
          content: 'Page № 13'
        },
        {
          content: 'Page № 14'
        }
      ]
    }
  },
  methods: {
    test: function (e) {
      console.log(e)
    },
    callMethod: function (e) {
      console.log(e)
    }
  },
  computed: {
    settings: function () {
      return {
        array: this.pages,
        pageClass: 'test-class',
        hideArrows: false,
        controlStyle: 'circle1',
        maxButtons: 5,
        pageButtons: {
          'background': '',
          'borderColor': '',
          'color': '',
          'backgroundHover': '',
          'borderColorHover': '',
          'colorHover': ''
        },
        currentPageButton: {
          'backgroundActive': '',
          'borderColorActive': '',
          'colorActive': ''
        },
        controlClass: '',
        arrowStyle: 'styleArrow-2',
        controlDotsStyle: 'style1',
        arrowStyleColor: 'red',
        spinner: true,
        spinnerStyle: 'spinnerStyle-2',
        spinnerColor: 'white',
        pageStarted: 1
      }
    }
  }
}
</script>
