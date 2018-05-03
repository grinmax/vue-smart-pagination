<template>
  <div>
    <slot></slot>
    {{maxButton}}
    <ul class="pagination-list"
        :class="[
          settings.controlClass
        ]"
    >
      <li class="pagination-list__li">
        <button
                v-if="settings.hideArrows != true"
                @click="switch_page(curIndex - 1)"
                class="pagination-list__button pagination-list__arrow pagination-list__arrow_prev"
                :class="[
                  {'pagination-list__button_disabled': curIndex === 0}
                ]"
                :style="[
                    settings.arrowColor ? {'border-color': settings.arrowColor} : {'border-color': '#e1e1e1'}
                ]"
        >
          &raquo;
        </button>
      </li>
      <template v-for="(item, index) in settings.array">
        <li class="pagination-list__li" v-if="test(index).li">
          <template v-if="test(index).button">
            <button
              :class="[
                {'pagination-list__button_page_active': curIndex === index }
              ]"
              :style="[
                  settings.pageButtons ? {'background': settings.pageButtons.background} : {'background': '#fff'},
                  settings.pageButtons ? {'borderColor': settings.pageButtons.borderColor} : {'border-color': '#02C8F3'},
                  settings.pageButtons ? {'color': settings.pageButtons.color} : {'color': '#02C8F3'}
              ]"
              @click="[
                switch_page(index)
              ]"
              class="pagination-list__button pagination-list__button_page">{{ index + 1 }}
            </button>
          </template>
          <template v-else>
            ...
          </template>
        </li>
      </template>
      <li class="pagination-list__li">
        <button
                v-if="settings.hideArrows != true"
                @click="switch_page(curIndex + 1)"
                class="pagination-list__button pagination-list__arrow pagination-list__arrow_next"
                :class="[
                  {'pagination-list__button_disabled': curIndex === settings.array.length - 1}
                ]"
                :style="[
                    settings.arrowColor ? {'border-color': settings.arrowColor} : {'border-color': '#e1e1e1'}
                ]"
          >
          &raquo;
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
      show: ''
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
    switch_page: function (index) {
      this.curIndex = index
      for (let i = 0; i < this.settings.array.length; i++) {
        this.$set(this.settings.array[i], 'active', false)
      }
      this.$set(this.settings.array[index], 'active', true)
    },
    test: function (index) {
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
    this.$set(this.settings.array[0], 'active', true)
    let root = document.querySelector(':root')
    if (this.settings.arrowColor) {
      root.style.setProperty('--arrowColor', this.settings.arrowColor)
    }
    if (this.settings.controlStyle === 'square') {
      root.style.setProperty('--controlStyle', '0')
    }
    if (this.settings.controlStyle === 'circle') {
      root.style.setProperty('--controlStyle', '50%')
    } else {
      root.style.setProperty('--controlStyle', '4px')
    }
  }
}
</script>

<style lang="scss">

  :root {
    --arrowColor: red;
    --controlStyle: 0;
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
      background-color: #ffffff;
      color: #9da0a2;
      /*color: var(--arrowColor);*/
      transition: border-color .2s ease-in, background-color .2s ease-in;
      cursor: pointer;
      /*border-radius: 4px;*/
      outline: none;
      border: solid 1px #e1e1e1;
      border-radius: var(--controlStyle);
      &_disabled {
        opacity: 0;
        pointer-events: none;
      }

      &_page {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        color: #02C8F3;
        border: 1px solid #02C8F3;
        font-size: 15px;

        &:hover{
          border-color: #02C8F3;
          color: #ffffff;
          background-color: #02C8F3;
        }

        &_active {
          border-color: #e1e1e1;
          color: #ffffff;
          background-color: #02C8F3;
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
      }
    }

    &__arrow {
      font-size: 18px;
      background: none;
      transition: opacity .2s ease-in;

      &:focus, &:active {
        border-color: #e1e1e1;
      }

      &_prev {
        transform: scaleX(-1);
      }

      &:hover {
        color: #02C8F3;
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
    width: 100%;
    padding-top: 15px;
    padding-bottom: 15px;
    user-select: none;

    &__page {
      border: solid 1px #e1e1e1;
      margin-bottom: 30px;
      padding: 50px;
      text-align: center;
      font-family: 'Avenir', Helvetica, Arial, sans-serif;
      font-size: 20px;
    }

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
</style>
