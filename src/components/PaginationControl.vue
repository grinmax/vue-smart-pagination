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
          <svg v-if="this.settings.arrowStyle === 'styleArrow-1'" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1"
               id="Capa_1" x="0px" y="0px" viewBox="0 0 31.49 31.49" style="enable-background:new 0 0 31.49 31.49;"
               xml:space="preserve" width="40px" height="40px" class="">
            <g>
              <path d="M21.205,5.007c-0.429-0.444-1.143-0.444-1.587,0c-0.429,0.429-0.429,1.143,0,1.571l8.047,8.047H1.111  C0.492,14.626,0,15.118,0,15.737c0,0.619,0.492,1.127,1.111,1.127h26.554l-8.047,8.032c-0.429,0.444-0.429,1.159,0,1.587  c0.444,0.444,1.159,0.444,1.587,0l9.952-9.952c0.444-0.429,0.444-1.143,0-1.571L21.205,5.007z"
                    data-original="#1E201D" class="active-path" data-old_color="#242423" fill="red"/>
            </g>
          </svg>
          <!--<svg v-else-if="this.settings.arrowStyle === 'styleArrow-2'" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" id="Capa_1" x="0px" y="0px" viewBox="0 0 54 54" style="enable-background:new 0 0 54 54;" xml:space="preserve" width="40px" height="40px" class=""><g><g>-->
              <!--<g>-->
                <!--<rect x="1" y="1" :style="[this.settings.arrowStyleColor ? {fill : this.settings.arrowStyleColor} : {fill: '#02C8F3' }]" width="52" height="52" data-original="#687492" class=""/>-->
                <!--<path style="fill:#fff" d="M54,54H0V0h54V54z M2,52h50V2H2V52z" data-original="#687492" class=""/>-->
              <!--</g>-->
              <!--<path style="fill:#FFFFFF" d="M19,45c-0.256,0-0.512-0.098-0.707-0.293c-0.391-0.391-0.391-1.023,0-1.414L34.586,27L18.293,10.707   c-0.391-0.391-0.391-1.023,0-1.414s1.023-0.391,1.414,0L37.414,27L19.707,44.707C19.512,44.902,19.256,45,19,45z" data-original="#FFFFFF" class="active-path"/>-->
            <!--</g></g>-->
          <!--</svg>-->
          <svg v-else-if="this.settings.arrowStyle === 'styleArrow-2'" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" id="Capa_1" x="0px" y="0px" width="40px" height="40px" viewBox="0 0 284.929 284.929" style="enable-background:new 0 0 284.929 284.929;" xml:space="preserve" class=""><g transform="matrix(-1 1.22465e-16 -1.22465e-16 -1 284.929 284.929)"><g>
              <g>
                <path d="M165.304,142.468L277.517,30.267c1.902-1.903,2.847-4.093,2.847-6.567c0-2.475-0.951-4.665-2.847-6.567L263.239,2.857    C261.337,0.955,259.146,0,256.676,0c-2.478,0-4.665,0.955-6.571,2.857L117.057,135.9c-1.903,1.903-2.853,4.093-2.853,6.567    c0,2.475,0.95,4.664,2.853,6.567l133.048,133.043c1.903,1.906,4.086,2.851,6.564,2.851c2.478,0,4.66-0.947,6.563-2.851    l14.277-14.267c1.902-1.903,2.851-4.094,2.851-6.57c0-2.472-0.948-4.661-2.851-6.564L165.304,142.468z" data-original="#000000" class="active-path" fill="#000000"/>
                <path d="M55.668,142.468L167.87,30.267c1.903-1.903,2.851-4.093,2.851-6.567c0-2.475-0.947-4.665-2.851-6.567L153.6,2.857    C151.697,0.955,149.507,0,147.036,0c-2.478,0-4.668,0.955-6.57,2.857L7.417,135.9c-1.903,1.903-2.853,4.093-2.853,6.567    c0,2.475,0.95,4.664,2.853,6.567l133.048,133.043c1.902,1.906,4.09,2.851,6.57,2.851c2.471,0,4.661-0.947,6.563-2.851    l14.271-14.267c1.903-1.903,2.851-4.094,2.851-6.57c0-2.472-0.947-4.661-2.851-6.564L55.668,142.468z" data-original="#000000" class="active-path" fill="#000000"/>
              </g>
            </g></g>
          </svg>

          <svg v-else-if="this.settings.arrowStyle === 'styleArrow-3'" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" id="Capa_1" x="0px" y="0px" viewBox="0 0 54 54" style="enable-background:new 0 0 54 54;" xml:space="preserve" width="40px" height="40px"><g><g>
              <g>
                <path :style="[this.settings.arrowStyleColor ? {fill : this.settings.arrowStyleColor} : {fill: '#02C8F3' }]" d="M27,53L27,53C12.641,53,1,41.359,1,27v0C1,12.641,12.641,1,27,1h0c14.359,0,26,11.641,26,26v0    C53,41.359,41.359,53,27,53z" data-original="#9B507E"/>
                <path :style="[this.settings.arrowStyleColor ? {fill : this.settings.arrowStyleColor} : {fill: '#02C8F3' }]" d="M27,54C12.112,54,0,41.888,0,27S12.112,0,27,0s27,12.112,27,27S41.888,54,27,54z M27,2    C13.215,2,2,13.215,2,27s11.215,25,25,25s25-11.215,25-25S40.785,2,27,2z" data-original="#9B507E"/>
              </g>
                <path style="fill:#FFFFFF" d="M39,28H13c-0.552,0-1-0.447-1-1s0.448-1,1-1h26c0.552,0,1,0.447,1,1S39.552,28,39,28z" data-original="#FFFFFF" class="active-path"/>
                <polygon style="fill:#FFFFFF" points="30.707,37.707 29.293,36.293 38.586,27 29.293,17.707 30.707,16.293 41.414,27  " data-original="#FFFFFF" class="active-path"/>
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
            <svg v-if="this.settings.arrowStyle === 'styleArrow-1'" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1"
                 id="Capa_1" x="0px" y="0px" viewBox="0 0 31.49 31.49" style="enable-background:new 0 0 31.49 31.49;"
                 xml:space="preserve" width="40px" height="40px" class="">
              <g>
                <path d="M21.205,5.007c-0.429-0.444-1.143-0.444-1.587,0c-0.429,0.429-0.429,1.143,0,1.571l8.047,8.047H1.111  C0.492,14.626,0,15.118,0,15.737c0,0.619,0.492,1.127,1.111,1.127h26.554l-8.047,8.032c-0.429,0.444-0.429,1.159,0,1.587  c0.444,0.444,1.159,0.444,1.587,0l9.952-9.952c0.444-0.429,0.444-1.143,0-1.571L21.205,5.007z"
                      data-original="#1E201D" class="active-path" data-old_color="#242423" fill="red"/>
              </g>
            </svg>
            <!--<svg v-else-if="this.settings.arrowStyle === 'styleArrow-2'" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" id="Capa_1" x="0px" y="0px" viewBox="0 0 54 54" style="enable-background:new 0 0 54 54;" xml:space="preserve" width="40px" height="40px" class=""><g><g>-->
                <!--<g>-->
                  <!--<rect x="1" y="1" :style="[this.settings.arrowStyleColor ? {fill : this.settings.arrowStyleColor} : {fill: '#02C8F3' }]" width="52" height="52" data-original="#687492" class=""/>-->
                  <!--<path style="fill:#fff" d="M54,54H0V0h54V54z M2,52h50V2H2V52z" data-original="#687492" class=""/>-->
                <!--</g>-->
                <!--<path style="fill:#FFFFFF" d="M19,45c-0.256,0-0.512-0.098-0.707-0.293c-0.391-0.391-0.391-1.023,0-1.414L34.586,27L18.293,10.707   c-0.391-0.391-0.391-1.023,0-1.414s1.023-0.391,1.414,0L37.414,27L19.707,44.707C19.512,44.902,19.256,45,19,45z" data-original="#FFFFFF" class="active-path"/>-->
              <!--</g></g>-->
            <!--</svg>-->
            <svg v-else-if="this.settings.arrowStyle === 'styleArrow-2'" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" id="Capa_1" x="0px" y="0px" width="40px" height="40px" viewBox="0 0 284.929 284.929" style="enable-background:new 0 0 284.929 284.929;" xml:space="preserve" class=""><g transform="matrix(-1 1.22465e-16 -1.22465e-16 -1 284.929 284.929)"><g>
                <g>
                  <path d="M165.304,142.468L277.517,30.267c1.902-1.903,2.847-4.093,2.847-6.567c0-2.475-0.951-4.665-2.847-6.567L263.239,2.857    C261.337,0.955,259.146,0,256.676,0c-2.478,0-4.665,0.955-6.571,2.857L117.057,135.9c-1.903,1.903-2.853,4.093-2.853,6.567    c0,2.475,0.95,4.664,2.853,6.567l133.048,133.043c1.903,1.906,4.086,2.851,6.564,2.851c2.478,0,4.66-0.947,6.563-2.851    l14.277-14.267c1.902-1.903,2.851-4.094,2.851-6.57c0-2.472-0.948-4.661-2.851-6.564L165.304,142.468z" data-original="#000000" class="active-path" fill="#000000"/>
                  <path d="M55.668,142.468L167.87,30.267c1.903-1.903,2.851-4.093,2.851-6.567c0-2.475-0.947-4.665-2.851-6.567L153.6,2.857    C151.697,0.955,149.507,0,147.036,0c-2.478,0-4.668,0.955-6.57,2.857L7.417,135.9c-1.903,1.903-2.853,4.093-2.853,6.567    c0,2.475,0.95,4.664,2.853,6.567l133.048,133.043c1.902,1.906,4.09,2.851,6.57,2.851c2.471,0,4.661-0.947,6.563-2.851    l14.271-14.267c1.903-1.903,2.851-4.094,2.851-6.57c0-2.472-0.947-4.661-2.851-6.564L55.668,142.468z" data-original="#000000" class="active-path" fill="#000000"/>
                </g>
              </g></g>
            </svg>
            <svg v-else xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" version="1.1" id="Capa_1" x="0px" y="0px" viewBox="0 0 54 54" style="enable-background:new 0 0 54 54;" xml:space="preserve" width="40px" height="40px"><g><g>
                <g>
                  <path :style="[this.settings.arrowStyleColor ? {fill : this.settings.arrowStyleColor} : {fill: '#02C8F3' }]" d="M27,53L27,53C12.641,53,1,41.359,1,27v0C1,12.641,12.641,1,27,1h0c14.359,0,26,11.641,26,26v0    C53,41.359,41.359,53,27,53z" data-original="#9B507E"/>
                  <path :style="[this.settings.arrowStyleColor ? {fill : this.settings.arrowStyleColor} : {fill: '#02C8F3' }]" d="M27,54C12.112,54,0,41.888,0,27S12.112,0,27,0s27,12.112,27,27S41.888,54,27,54z M27,2    C13.215,2,2,13.215,2,27s11.215,25,25,25s25-11.215,25-25S40.785,2,27,2z" data-original="#9B507E"/>
                </g>
                  <path style="fill:#FFFFFF" d="M39,28H13c-0.552,0-1-0.447-1-1s0.448-1,1-1h26c0.552,0,1,0.447,1,1S39.552,28,39,28z" data-original="#FFFFFF" class="active-path"/>
                  <polygon style="fill:#FFFFFF" points="30.707,37.707 29.293,36.293 38.586,27 29.293,17.707 30.707,16.293 41.414,27  " data-original="#FFFFFF" class="active-path"/>
              </g></g>
            </svg>
        </button>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: 'PaginationControl',
  data: function () {
    return {
      curIndex: 0,
      activeItemId: '',
      show: '',
      testing: ''
    }
  },
  props: ['settings'],
  computed: {
    maxButton: function () {
      if (!isNaN(this.settings.maxButtons % 2)) {
        console.log(this.settings.maxButtons % 2)
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
      if (this.settings.controlDotsStyle === 'style1') {
        return 'pagination-list__button_dots-style-1'
      } else if (this.settings.controlDotsStyle === 'style2') {
        return 'pagination-list__button_dots-style-2'
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
      this.$set(this.settings.array[this.settings.pageStarted - 1], 'active', true)
    }
    let root = document.querySelector(':root')
    if (this.settings.controlStyle === 'square') {
      root.style.setProperty('--controlStyle', '0')
    } else if (this.settings.controlStyle === 'circle') {
      root.style.setProperty('--controlStyle', '50%')
    } else {
      root.style.setProperty('--controlStyle', '4px')
    }
    if (this.settings.pageButtons.background) {
      root.style.setProperty('--pageButtonsBackground', this.settings.pageButtons.background)
    }
    if (this.settings.pageButtons.borderColor) {
      root.style.setProperty('--pageButtonsBorderColor', this.settings.pageButtons.borderColor)
    }
    if (this.settings.pageButtons.color) {
      root.style.setProperty('--pageButtonsColor', this.settings.pageButtons.color)
    }
    if (this.settings.pageButtons.backgroundHover) {
      root.style.setProperty('--pageButtonsBackgroundHover', this.settings.pageButtons.backgroundHover)
    }
    if (this.settings.pageButtons.borderColorHover) {
      root.style.setProperty('--pageButtonsBorderColorHover', this.settings.pageButtons.borderColorHover)
    }
    if (this.settings.pageButtons.colorHover) {
      root.style.setProperty('--pageButtonsColorHover', this.settings.pageButtons.colorHover)
    }
    if (this.settings.currentPageButton.backgroundActive) {
      root.style.setProperty('--pageButtonBackgroundActive', this.settings.currentPageButton.backgroundActive)
    }
    if (this.settings.currentPageButton.borderColorActive) {
      root.style.setProperty('--pageButtonBorderColorActive', this.settings.currentPageButton.borderColorActive)
    }
    if (this.settings.currentPageButton.colorActive) {
      root.style.setProperty('--pageButtonColorActive', this.settings.currentPageButton.colorActive)
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
    --pageButtonsBorderColorHover: #e1e1e1;
    --pageButtonsColorHover: #fff;
    --pageButtonBackgroundActive: #02C8F3;
    --pageButtonBorderColorActive: #e1e1e1;
    --pageButtonColorActive: #fff;
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
            border-color: #e1e1e1;
          }
        }
      }

      &_dots {
        font-size: 24px;
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        color: #02C8F3;
        background: none;
        &-style-1 {
          color: #fff;
          height: 40px;
        }
        &-style-2 {
          color: #000;
          height: 40px;
        }
      }
    }

    &__arrow {
      font-size: 18px;
      background: var(--pageArrowsBackground);
      color: var(--pageArrowsColor);
      transition: opacity, background .2s ease-in;
      border: 1px solid var(--pageArrowsBorderColor);
      padding: 0;
      border: none;

      &:focus, &:active {
        border-color: var(--pageArrowsBorderColorHover);
      }

      &_prev {
        transform: scaleX(-1);
      }

      &:hover {
        background: var(--pageArrowsBackgroundHover);
        border-color: var(--pageArrowsBorderColorHover);
        color: var(--pageArrowsColorHover);
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
    &:hover {
      opacity:.7;
    }
  }
</style>
