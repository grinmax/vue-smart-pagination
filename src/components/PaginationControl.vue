<template>
  <div>
    <slot></slot>
    <ul class="pagination-list"
        :class="[
          settings.controlClass
        ]"
    >
      <li class="pagination-list__li">
        <button
                v-if="settings.hideArrows != true"
                @click="[
                  switch_page(curIndex - 1),
                ]"
                class="pagination-list__button pagination-list__arrow pagination-list__arrow_prev"
                :class="[
                  {'pagination-list__button_disabled': curIndex === 0},
                  styleArrows()
                ]"
        >
          <svg v-if="this.settings.arrowStyle ? this.settings.arrowStyle === 'styleArrow-1' : 'styleArrow-1'" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1"
               id="Capa_1" x="0" y="0" viewBox="0 0 31.49 31.49" style="enable-background:new 0 0 31.49 31.49;"
               xml:space="preserve" width="15px" height="15px" class=""
               :style="[this.settings.arrowStyleColor ? {fill : this.settings.arrowStyleColor} : {fill: '#02C8F3' }]"
          >
            <g>
              <path  d="M21.205,5.007c-0.429-0.444-1.143-0.444-1.587,0c-0.429,0.429-0.429,1.143,0,1.571l8.047,8.047H1.111  C0.492,14.626,0,15.118,0,15.737c0,0.619,0.492,1.127,1.111,1.127h26.554l-8.047,8.032c-0.429,0.444-0.429,1.159,0,1.587  c0.444,0.444,1.159,0.444,1.587,0l9.952-9.952c0.444-0.429,0.444-1.143,0-1.571L21.205,5.007z"
                    data-original="#1E201D" class="active-path" data-old_color="#242423" />
            </g>
          </svg>
          <svg :style="[this.settings.arrowStyleColor ? {fill : this.settings.arrowStyleColor} : {fill: '#02C8F3' }]" v-else-if="this.settings.arrowStyle === 'styleArrow-2'" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" id="Capa_1" x="0" y="0" width="10px" height="10px" viewBox="0 0 284.929 284.929" style="enable-background:new 0 0 284.929 284.929;" xml:space="preserve" class=""><g transform="matrix(-1 1.22465e-16 -1.22465e-16 -1 284.929 284.929)"><g>
              <g>
                <path d="M165.304,142.468L277.517,30.267c1.902-1.903,2.847-4.093,2.847-6.567c0-2.475-0.951-4.665-2.847-6.567L263.239,2.857    C261.337,0.955,259.146,0,256.676,0c-2.478,0-4.665,0.955-6.571,2.857L117.057,135.9c-1.903,1.903-2.853,4.093-2.853,6.567    c0,2.475,0.95,4.664,2.853,6.567l133.048,133.043c1.903,1.906,4.086,2.851,6.564,2.851c2.478,0,4.66-0.947,6.563-2.851    l14.277-14.267c1.902-1.903,2.851-4.094,2.851-6.57c0-2.472-0.948-4.661-2.851-6.564L165.304,142.468z" data-original="#000000" class="active-path"/>
                <path d="M55.668,142.468L167.87,30.267c1.903-1.903,2.851-4.093,2.851-6.567c0-2.475-0.947-4.665-2.851-6.567L153.6,2.857    C151.697,0.955,149.507,0,147.036,0c-2.478,0-4.668,0.955-6.57,2.857L7.417,135.9c-1.903,1.903-2.853,4.093-2.853,6.567    c0,2.475,0.95,4.664,2.853,6.567l133.048,133.043c1.902,1.906,4.09,2.851,6.57,2.851c2.471,0,4.661-0.947,6.563-2.851    l14.271-14.267c1.903-1.903,2.851-4.094,2.851-6.57c0-2.472-0.947-4.661-2.851-6.564L55.668,142.468z" data-original="#000000" class="active-path"/>
              </g>
            </g></g>
          </svg>
          <svg :style="[this.settings.arrowStyleColor ? {fill : this.settings.arrowStyleColor} : {fill: '#02C8F3' }]" v-if="this.settings.arrowStyle === 'styleArrow-3'" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" id="Capa_1" x="0" y="0" viewBox="0 0 443.52 443.52" style="enable-background:new 0 0 443.52 443.52;" xml:space="preserve" width="10px" height="10px"><g transform="matrix(-1 1.22465e-16 -1.22465e-16 -1 443.52 443.52)"><g>
              <g>
                <path d="M143.492,221.863L336.226,29.129c6.663-6.664,6.663-17.468,0-24.132c-6.665-6.662-17.468-6.662-24.132,0l-204.8,204.8    c-6.662,6.664-6.662,17.468,0,24.132l204.8,204.8c6.78,6.548,17.584,6.36,24.132-0.42c6.387-6.614,6.387-17.099,0-23.712    L143.492,221.863z" data-original="#000000" class="active-path"/>
              </g>
            </g></g>
          </svg>

        </button>
      </li>
      <template v-for="(item, index) in settings.array">
        <li class="pagination-list__li" v-if="pagination(index).li" :key="index">
          <template v-if="pagination(index).button">
            <button
              :class="[
                {'pagination-list__button_page_active': curIndex === index}
              ]"
              @click="[
                switch_page(index)
              ]"
              class="pagination-list__button pagination-list__button_page">{{ index + 1 }}
            </button>
          </template>
          <template v-else>
            <div class="pagination-list__button_dots"
                 :class="styleDots()">
              ...
            </div>
          </template>
        </li>
      </template>
      <li class="pagination-list__li">
        <button
                v-if="settings.hideArrows != true"
                @click="[
                  switch_page(curIndex + 1)
                  ]"
                class="pagination-list__button pagination-list__arrow pagination-list__arrow_next"
                :class="[
                  {'pagination-list__button_disabled': curIndex === settings.array.length - 1},
                  styleArrows()
                ]"
          >
            <svg :style="[this.settings.arrowStyleColor ? {fill : this.settings.arrowStyleColor} : {fill: '#02C8F3' }]" v-if="this.settings.arrowStyle ? this.settings.arrowStyle === 'styleArrow-1' : 'styleArrow-1'" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1"
                 id="Capa_1" x="0" y="0" viewBox="0 0 31.49 31.49" style="enable-background:new 0 0 31.49 31.49;"
                 xml:space="preserve" width="15px" height="15px" class="">
              <g>
                <path d="M21.205,5.007c-0.429-0.444-1.143-0.444-1.587,0c-0.429,0.429-0.429,1.143,0,1.571l8.047,8.047H1.111  C0.492,14.626,0,15.118,0,15.737c0,0.619,0.492,1.127,1.111,1.127h26.554l-8.047,8.032c-0.429,0.444-0.429,1.159,0,1.587  c0.444,0.444,1.159,0.444,1.587,0l9.952-9.952c0.444-0.429,0.444-1.143,0-1.571L21.205,5.007z"
                      data-original="#1E201D" class="active-path" data-old_color="#242423"/>
              </g>
            </svg>
            <svg :style="[this.settings.arrowStyleColor ? {fill : this.settings.arrowStyleColor} : {fill: '#02C8F3' }]" v-else-if="this.settings.arrowStyle === 'styleArrow-2'" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" id="Capa_1" x="0" y="0" width="10px" height="10px" viewBox="0 0 284.929 284.929" style="enable-background:new 0 0 284.929 284.929;" xml:space="preserve" class=""><g transform="matrix(-1 1.22465e-16 -1.22465e-16 -1 284.929 284.929)"><g>
                <g>
                  <path d="M165.304,142.468L277.517,30.267c1.902-1.903,2.847-4.093,2.847-6.567c0-2.475-0.951-4.665-2.847-6.567L263.239,2.857    C261.337,0.955,259.146,0,256.676,0c-2.478,0-4.665,0.955-6.571,2.857L117.057,135.9c-1.903,1.903-2.853,4.093-2.853,6.567    c0,2.475,0.95,4.664,2.853,6.567l133.048,133.043c1.903,1.906,4.086,2.851,6.564,2.851c2.478,0,4.66-0.947,6.563-2.851    l14.277-14.267c1.902-1.903,2.851-4.094,2.851-6.57c0-2.472-0.948-4.661-2.851-6.564L165.304,142.468z" data-original="#000000" class="active-path"/>
                  <path d="M55.668,142.468L167.87,30.267c1.903-1.903,2.851-4.093,2.851-6.567c0-2.475-0.947-4.665-2.851-6.567L153.6,2.857    C151.697,0.955,149.507,0,147.036,0c-2.478,0-4.668,0.955-6.57,2.857L7.417,135.9c-1.903,1.903-2.853,4.093-2.853,6.567    c0,2.475,0.95,4.664,2.853,6.567l133.048,133.043c1.902,1.906,4.09,2.851,6.57,2.851c2.471,0,4.661-0.947,6.563-2.851    l14.271-14.267c1.903-1.903,2.851-4.094,2.851-6.57c0-2.472-0.947-4.661-2.851-6.564L55.668,142.468z" data-original="#000000" class="active-path"/>
                </g>
              </g></g>
            </svg>
            <svg :style="[this.settings.arrowStyleColor ? {fill : this.settings.arrowStyleColor} : {fill: '#02C8F3' }]" v-if="this.settings.arrowStyle === 'styleArrow-3'" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" id="Capa_1" x="0" y="0" viewBox="0 0 443.52 443.52" style="enable-background:new 0 0 443.52 443.52;" xml:space="preserve" width="10px" height="10px"><g transform="matrix(-1 1.22465e-16 -1.22465e-16 -1 443.52 443.52)"><g>
                <g>
                  <path d="M143.492,221.863L336.226,29.129c6.663-6.664,6.663-17.468,0-24.132c-6.665-6.662-17.468-6.662-24.132,0l-204.8,204.8    c-6.662,6.664-6.662,17.468,0,24.132l204.8,204.8c6.78,6.548,17.584,6.36,24.132-0.42c6.387-6.614,6.387-17.099,0-23.712    L143.492,221.863z" data-original="#000000" class="active-path"/>
                </g>
              </g></g>
            </svg>
        </button>
      </li>
    </ul>
  </div>
</template>
<script>
import { defaultsDeep } from 'lodash'

export default {
  name: 'PaginationControl',
  props: ['settings'],
  data: function () {
    return {
      curIndex: 0,
      activeItemId: '',
      show: '',
      testing: '',
      defValues: {
        pageButtons: {
          'background': '#fff',
          'borderColor': '#02C8F3',
          'color': '#02C8F3',
          'backgroundHover': '#02C8F3',
          'borderColorHover': '#02C8F3',
          'colorHover': '#fff'
        },
        currentPageButton: {
          'backgroundActive': '#02C8F3',
          'borderColorActive': '#02C8F3',
          'colorActive': '#fff'
        },
        pageDots: {
          'controlDotsColor': '#000'
        },
        pageArrows: {
          'arrowStyleColorHover': '#fff'
        }
      }
    }
  },
  computed: {
    def: function () {
      return defaultsDeep(this.settings.style, this.defValues)
    },
    maxButton: function () {
      if (!isNaN(this.settings.maxButtons % 2)) {
        if (this.settings.maxButtons % 2 === 0) {
          return this.settings.maxButtons + 1
        } else return this.settings.maxButtons
      } else {
        return 5
      }
    }
  },
  methods: {
    keydown: function (e) {
      if (e.ctrlKey && e.which === 39 && this.curIndex < this.settings.array.length - 1) {
        this.switch_page(this.curIndex + 1)
      }
      if (e.ctrlKey && e.which === 37 && this.curIndex > 0) {
        this.switch_page(this.curIndex - 1)
      }
    },
    styleDots: function () {
      if (this.settings.controlDotsStyle === 'styleDots-1') {
        return 'pagination-list__button_dots-style-1'
      } else if (this.settings.controlDotsStyle === 'styleDots-2') {
        return 'pagination-list__button_dots-style-2'
      } else if (this.settings.controlDotsStyle === 'styleDots-3') {
        return 'pagination-list__button_dots-style-3'
      } else {
        return 'pagination-list__button_dots-style-1'
      }
    },
    styleArrows: function () {
      if (this.settings.arrowStyle === 'styleArrow-1') {
        return 'styleArrow-1'
      } else if (this.settings.arrowStyle === 'styleArrow-2') {
        return 'styleArrow-2'
      } else {
        return 'styleArrow-3'
      }
    },
    switch_page: function (index) {
      this.curIndex = index
      for (let i = 0; i < this.settings.array.length; i++) {
        this.$set(this.settings.array[i], 'active', false)
      }
      this.$set(this.settings.array[index], 'active', true)
      this.$emit('callMethod', index)
    },
    pagination: function (index) {
      if (index === 0 || index === this.settings.array.length - 1) {
        return {
          li: true,
          button: true
        }
      } else {
        if (this.curIndex === 0) {
          if (index <= this.maxButton - 2) {
            return {
              li: true,
              button: true
            }
          } else if (index === this.maxButton - 1) {
            return {
              li: true,
              button: false
            }
          } else {
            return {
              li: false
            }
          }
        } else {
          if (index === this.curIndex) {
            return {
              li: true,
              button: true
            }
          } else if (this.curIndex - this.maxButton / 2 + 1 <= 0) {
            if ((index <= this.curIndex + this.maxButton / 2 - 1 + (Math.abs(this.curIndex - this.maxButton / 2 + 1)) && (index >= this.curIndex - this.maxButton / 2 + 1))) {
              return {
                li: true,
                button: true
              }
            } else if (index === this.curIndex + Math.round(this.maxButton / 2) - 1 + (Math.abs(this.curIndex - Math.round(this.maxButton / 2) + 1)) || (index === this.curIndex - Math.round(this.maxButton / 2) + 1)) {
              return {
                li: true,
                button: false
              }
            } else {
              return {
                li: false
              }
            }
          } else if (this.curIndex + this.maxButton / 2 + 1 > this.settings.array.length) {
            if ((index <= this.curIndex + this.maxButton / 2 - 1) && (index >= this.curIndex - this.maxButton / 2 + 1 - (this.curIndex + Math.round(this.maxButton / 2) - this.settings.array.length))) {
              return {
                li: true,
                button: true
              }
            } else if (index === this.curIndex - Math.round(this.maxButton / 2) + 1 - (this.curIndex + Math.round(this.maxButton / 2) - this.settings.array.length)) {
              return {
                li: true,
                button: false
              }
            } else {
              return {
                li: false
              }
            }
          } else {
            if ((index <= this.curIndex + this.maxButton / 2 - 1) && (index >= this.curIndex - this.maxButton / 2 + 1)) {
              return {
                li: true,
                button: true
              }
            } else if ((index === this.curIndex + Math.round(this.maxButton / 2) - 1) || (index === this.curIndex - Math.round(this.maxButton / 2) + 1)) {
              return {
                li: true,
                button: false
              }
            } else {
              return {
                li: false
              }
            }
          }
        }
      }
    }
  },
  beforeMount () {
    document.addEventListener('keydown', this.keydown)
    if (this.settings.pageStarted) {
      this.curIndex = this.settings.pageStarted - 1
    } else {
      this.curIndex = 0
    }
    this.$set(this.settings.array[this.curIndex], 'active', true)
    let root = document.querySelector(':root')
    if (this.settings.controlStyle === 'square') {
      root.style.setProperty('--controlStyle', '0')
    } else if (this.settings.controlStyle === 'circle') {
      root.style.setProperty('--controlStyle', '50%')
    } else {
      root.style.setProperty('--controlStyle', '4px')
    }
    if (this.def.pageButtons.background) {
      root.style.setProperty('--pageButtonsBackground', this.def.pageButtons.background)
    }
    if (this.def.pageButtons.borderColor) {
      root.style.setProperty('--pageButtonsBorderColor', this.def.pageButtons.borderColor)
    }
    if (this.def.pageButtons.color) {
      root.style.setProperty('--pageButtonsColor', this.def.pageButtons.color)
    }
    if (this.def.pageButtons.backgroundHover) {
      root.style.setProperty('--pageButtonsBackgroundHover', this.def.pageButtons.backgroundHover)
    }
    if (this.def.pageButtons.borderColorHover) {
      root.style.setProperty('--pageButtonsBorderColorHover', this.def.pageButtons.borderColorHover)
    }
    if (this.def.pageButtons.colorHover) {
      root.style.setProperty('--pageButtonsColorHover', this.def.pageButtons.colorHover)
    }
    if (this.def.currentPageButton.backgroundActive) {
      root.style.setProperty('--pageButtonBackgroundActive', this.def.currentPageButton.backgroundActive)
    }
    if (this.def.currentPageButton.borderColorActive) {
      root.style.setProperty('--pageButtonBorderColorActive', this.def.currentPageButton.borderColorActive)
    }
    if (this.def.currentPageButton.colorActive) {
      root.style.setProperty('--pageButtonColorActive', this.def.currentPageButton.colorActive)
    }
    if (this.def.pageDots.controlDotsColor) {
      root.style.setProperty('--controlDotsColor', this.def.pageDots.controlDotsColor)
    }
    if (this.def.pageArrows.arrowStyleColorHover) {
      root.style.setProperty('--arrowStyleColorHover', this.def.pageArrows.arrowStyleColorHover)
    }
  }
}
</script>

<style lang="scss">

  :root {
    --controlStyle: 0;
    --pageButtonsBackground: #fff;
    --pageButtonsBorderColor: #02C8F3;
    --pageButtonsColor: #02C8F3;
    --pageButtonsBackgroundHover: #02C8F3;
    --pageButtonsBorderColorHover: #02C8F3;
    --pageButtonsColorHover: #fff;
    --pageButtonBackgroundActive: #02C8F3;
    --pageButtonBorderColorActive: #02C8F3;
    --pageButtonColorActive: #fff;
    --controlDotsColor: #000;
    --arrowStyleColorHover: #fff;
  }
  .pagination-list {
    display: flex;
    align-items: center;
    margin: 0;
    padding: 0;
    justify-content: center;
    user-select: none;

    li {
      list-style-type: none;
    }

    &__li {
      list-style-type: none;

      &+& {
        margin-left: 10px;
      }
    }

    &__button {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 40px;
      height: 40px;
      transition: border-color .2s ease-in, background-color .2s ease-in;
      cursor: pointer;
      outline: none;
      border-radius: var(--controlStyle);
      background: var(--pageButtonsBackground);

      &:hover {
        background-color: var(--pageButtonsBackgroundHover);
        border-color: var(--pageButtonsBorderColorHover);
      }

      &_disabled {
        opacity: 0;
        pointer-events: none;
      }

      &_page {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        border: solid 1px var(--pageButtonsBorderColor);
        color: var(--pageButtonsColor);
        font-size: 15px;

        &:hover{
          border-color: var(--pageButtonsBorderColorHover);
          color: var(--pageButtonsColorHover);
        }

        &_active {
          border-color: var(--pageButtonBorderColorActive);
          color: var(--pageButtonColorActive);
          background-color: var(--pageButtonBackgroundActive);
          pointer-events: none;

          &:focus {
            border-color: var(--pageButtonBorderColorActive);
          }
        }
      }

      &_dots {
        color: var(--controlDotsColor);
        &-style-1 {
          height: 60px;
          font-size: 30px;
          font-family: "Comic Sans MS", sans-serif;
          font-style: italic;
        }
        &-style-2 {
          height: 40px;
          font-size: 30px;
          font-weight: bold;
          font-family: 'Palatino Linotype', sans-serif;
        }
        &-style-3 {
          font-size: 20px;
          font-family: 'Avenir', Helvetica, Arial, sans-serif;
          background: none;
          height:20px;
        }
      }
    }

    &__arrow {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 40px;
      height: 40px;
      transition: border-color .2s ease-in, background-color .2s ease-in;
      cursor: pointer;
      outline: none;
      border-radius: var(--controlStyle);
      background: var(--pageButtonsBackground);
      font-family: 'Avenir', Helvetica, Arial, sans-serif;
      border: solid 1px var(--pageButtonsBorderColor);
      color: var(--pageButtonsColor);
      font-size: 15px;

      &:focus {
        border-color: var(--pageButtonsBorderColorHover);
        background-color: var(--pageButtonsBackgroundHover);
      }
      &:hover svg, &:focus svg {
        fill: var(--arrowStyleColorHover) !important;
      }
      &_prev {
        transform: scaleX(-1);
      }

      &_text {
        width: auto;

        span {
          font-size: 13px;
          font-family: 'Avenir', Helvetica, Arial, sans-serif;
          color: #02C8F3;
        }
      }
    }
  }

  .pagination-block {
    &__navigation {
      display: flex;
      align-items: center;
      justify-content: center;
      max-width: 100%;
    }
  }
  .pagination-img {
    text-align: center;
    img{
      max-width: 100%;
      height: auto;
    }
  }
  svg{
    transition: .2s;
  }
</style>
