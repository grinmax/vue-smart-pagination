<template>
  <div id="app">
    <div class="pagination-img">
      <img src="./assets/logo.png">
    </div>
    <pagination-page :settings="settings" />
    <pagination-control :settings="settings"/>
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
  computed: {
    settings: function () {
      return {
        array: this.pages,
        maxButtons: 5,
        pageClass: 'pageClass-test',
        hideArrows: false,
        controlStyle: 'circle',
        controlClass: 'controlClass-test',
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
        controlDotsStyle: 'style2',
        arrowStyle: 'styleArrow-1',
        arrowStyleColor: '#02C8F3',
        spinner: true,
        spinnerStyle: 'spinnerStyle-1',
        spinnerColor: 'white',
        pageStarted: 6
      }
    }
  }
}
</script>
