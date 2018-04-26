<template>
  <div class="pagination-block">
    <div class="pagination-block__page">
      <slot></slot>
    </div>
    <div class="pagination-block__navigation">
      <ul class="pagination-list">
        <template>
          <li class="pagination-list__li">
            <button class="pagination-list__button pagination-list__arrow pagination-list__arrow_prev">
              &raquo;
            </button>
          </li>
        </template>

        <template>
          <li class="pagination-list__li">
            <button class="pagination-list__button pagination-list__button_page">
              1
            </button>
          </li>
          <li>
            <button class="pagination-list__button pagination-list__button_dots">...</button>
          </li>
          <li class="pagination-list__li">
            <button class="pagination-list__button pagination-list__button_page">
              1
            </button>
          </li>
        </template>
        <template>
          <li class="pagination-list__li">
            <button class="pagination-list__button pagination-list__button_page">
              p - 1
            </button>
          </li>
        </template>
        <li class="pagination-list__li">
          <button class="pagination-list__button pagination-list__button_page pagination-list__button_page_active">
            p
          </button>
        </li>
        <template>
          <li class="pagination-list__li">
            <button class="pagination-list__button pagination-list__button_page">
              p + 1
            </button>
          </li>
        </template>

        <template>
          <li class="pagination-list__li">
            <button class="pagination-list__button pagination-list__button_page">
              3
            </button>
          </li>
          <li class="pagination-list__li">
            <button class="pagination-list__button pagination-list__button_page">
              4
            </button>
          </li>
          <li>
            <button class="pagination-list__button pagination-list__button_dots">...</button>
          </li>
          <li class="pagination-list__li">
            <button class="pagination-list__button pagination-list__button_page">
              Total
            </button>
          </li>
          <li class="pagination-list__li">
            <button class="pagination-list__button pagination-list__button_page">
              Total
            </button>
          </li>
        </template>

        <template>
          <li class="pagination-list__li">
            <button class="pagination-list__button pagination-list__arrow">
              &raquo;
            </button>
          </li>
        </template>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Pagination',
  props: ['paginationData', 'perPageData', 'perPageActive'],
  methods: {
    updatePage: function (val) {
      this.$emit('pageUpdate', val)
    },
    updatePerPage: function (val) {
      this.$emit('perPageUpdate', val)
    }
  }
}
</script>

<style lang="scss">
  .pagination-list {
    display: flex;
    align-items: center;
    margin: 0;
    padding: 0;

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
      transition: border-color .1s ease-in, background-color .1s ease-in;
      cursor: pointer;
      border-radius: 4px;
      outline: none;
      border: solid 1px #e1e1e1;

      &_page {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        color: #02C8F3;
        border: 1px solid #02C8F3;
        font-size: 15px;

        &:hover, &:focus, &:active {
          border-color: #02C8F3;
          color: #ffffff;
          background-color: #02C8F3;
        }

        &_active {
          border-color: #e1e1e1;
          color: #9da0a2;
          background: #ffffff;
          pointer-events: none;

          &:focus, &:active {
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
</style>
