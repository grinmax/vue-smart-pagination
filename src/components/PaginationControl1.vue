<template>
  <div>
    <slot></slot>
    {{maxButton}}
    <ul class="pagination-list">
      <li class="pagination-list__li">
        <button
                @click="switch_page(curIndex - 1)"
                class="pagination-list__button pagination-list__arrow pagination-list__arrow_prev"
                :class="[
                  {'pagination-list__button_disabled': curIndex === 0}
                ]"
                :style="[
                    settings.arrowColor ? {'border-color': settings.arrowColor} : {'border-color': '#e1e1e1'},
                    settings.hideArrows ? {'display': 'block'} : {'display': 'none'},
                    settings.controlsStyle ? {'border-radius': settings.controlsStyle} : {'border-radius': '4px'}
                ]"
        >
          &raquo;
        </button>
      </li>
      <template v-for="(item, index) in settings.array">
        <template v-if="index === 0 || index === settings.array.length - 1">
          <li class="pagination-list__li">
            <button
                    :class="{'pagination-list__button_page_active': curIndex === index }"
                    :style="[
                      settings.controlsStyle ? {'border-radius': settings.controlsStyle} : {'border-radius': '4px'}
                    ]"
                    @click="switch_page(index)"
                    class="pagination-list__button pagination-list__button_page">{{ index + 1 }}
            </button>
          </li>
        </template>
        <template v-else>
          <template v-if="(curIndex === 0)">
            <template v-if="(index <= maxButton - 2)">
              <li class="pagination-list__li">
                <button
                        :class="{'pagination-list__button_page_active': curIndex === index }"
                        :style="[
                          settings.controlsStyle ? {'border-radius': settings.controlsStyle} : {'border-radius': '4px'}
                        ]"
                        @click="switch_page(index)"
                        class="pagination-list__button pagination-list__button_page">
                  {{ index + 1 }}
                </button>
              </li>
            </template>
            <template v-else-if="index == maxButton - 1">
              <li class="pagination-list__li">
                ...
              </li>
            </template>
          </template>
          <template v-else>
            <template v-if="(index == curIndex)">
              <li class="pagination-list__li">
                <button
                        :class="{'pagination-list__button_page_active': curIndex === index }"
                        :style="[
                          settings.controlsStyle ? {'border-radius': settings.controlsStyle} : {'border-radius': '4px'}
                        ]"
                        @click="switch_page(index)"
                        class="pagination-list__button pagination-list__button_page">
                  {{ index + 1 }}
                </button>
              </li>
            </template>
            <template v-else-if="curIndex - maxButton / 2 + 1 <= 0">
              <template v-if="(index <= curIndex + maxButton / 2 - 1  + (Math.abs(curIndex - maxButton / 2 + 1))) && (index >= curIndex - maxButton / 2 + 1)">
                <li class="pagination-list__li">
                  <button
                          :class="{'pagination-list__button_page_active': curIndex === index }"
                          :style="[
                            settings.controlsStyle ? {'border-radius': settings.controlsStyle} : {'border-radius': '4px'}
                          ]"
                          @click="switch_page(index)"
                          class="pagination-list__button pagination-list__button_page">
                    {{ index + 1 }}
                  </button>
                </li>
              </template>
              <template v-else-if="(index ===  curIndex + Math.round(maxButton / 2) - 1 + (Math.abs(curIndex -  Math.round(maxButton / 2) + 1))) || (index === curIndex - Math.round(maxButton / 2) + 1)">
                <li class="pagination-list__li">
                  ...
                </li>
              </template>
            </template>
            <template v-else-if="curIndex + maxButton / 2 + 1 > settings.array.length">
              <template v-if="(index <= curIndex +maxButton / 2 - 1) && (index >= curIndex - maxButton / 2 + 1 - (curIndex + Math.round(maxButton / 2) - settings.array.length))">
                <li class="pagination-list__li">
                  <button
                          :class="{'pagination-list__button_page_active': curIndex === index }"
                          :style="[
                            settings.controlsStyle ? {'border-radius': settings.controlsStyle} : {'border-radius': '4px'}
                          ]"
                          @click="switch_page(index)"
                          class="pagination-list__button pagination-list__button_page">
                    {{ index + 1 }}
                  </button>
                </li>
              </template>
              <template v-else-if="(index ===  curIndex - Math.round(maxButton / 2) + 1 - (curIndex + Math.round(maxButton / 2) - settings.array.length))">
                <li class="pagination-list__li">
                  ...
                </li>
              </template>
            </template>
            <template v-else>
              <template v-if="(index <= curIndex +maxButton / 2 - 1) && (index >= curIndex - maxButton / 2 + 1)">
                <li class="pagination-list__li">
                  <button
                          :class="[
                            {'pagination-list__button_page_active': curIndex === index },
                            settings.controlClass
                            ]"
                          :style="[
                            settings.controlStyle ? {'border-radius': settings.controlStyle} : {'border-radius': '4px'}
                          ]"
                          @click="switch_page(index)"
                          class="pagination-list__button pagination-list__button_page">
                    {{ index + 1 }}
                  </button>
                </li>
              </template>
              <template v-else-if="(index ===  curIndex + Math.round(maxButton / 2) - 1) || (index === curIndex - Math.round(maxButton / 2) + 1)">
                <li class="pagination-list__li">
                  ...
                </li>
              </template>
            </template>
          </template>
        </template>
      </template>
      <li class="pagination-list__li">
        <button
                @click="switch_page(curIndex + 1)"
                class="pagination-list__button pagination-list__arrow pagination-list__arrow_next"
                :class="{'pagination-list__button_disabled': curIndex === settings.array.length - 1}"
                :style="[
                    settings.arrowColor ? {'border-color': settings.arrowColor} : {'border-color': '#e1e1e1'},
                    settings.hideArrows ? {'display': 'block'} : {'display': 'none'},
                    settings.controlsStyle ? {'border-radius': settings.controlsStyle} : {'border-radius': '4px'}
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
      activeItemId: ''
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
    }
  },
  beforeMount () {
    this.$set(this.settings.array[0], 'active', true)
  }
}
</script>

<style lang="scss">
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
      transition: border-color .2s ease-in, background-color .2s ease-in;
      cursor: pointer;
      border-radius: 4px;
      outline: none;
      border: solid 1px #e1e1e1;
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
