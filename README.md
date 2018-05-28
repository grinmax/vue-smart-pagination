
# Vue-smart-pagination
 A data pagination component that splits any data into pages and has many settings. All data is stored in an array and can have any value.

![img](https://github.com/grinmax/vue-smart-pagination/raw/master/src/assets/logo.png)

## Installation
 ### NPM Установите пакет npm.
```
$ npm install vue-smart-pagination --save
 ```
 Зарегистрируйте компонент.
* **ES5**
```js
var Pagination= require('vue-smart-pagination') Vue.component(pagination, Pagination)
 ```
* **ES6**
```js
  import Pagination from 'vue-smart-pagination' Vue.component('pagination', Pagination)
```
  ## Usage
Vue-smart-pagination состоит из двух основных компонентов:   **PaginationPage** - отвечает за вывод контента страницы.  **PaginationControl** - выводит кнопки контроля пагинацей.  Оба компонента регистрируются глобально после установки плагина.  Также существуют два основных объекта - `PaginationControlSettings` и  `PaginationPageSettings`. `PaginationControlSettings` содержит настройки, относящиеся к управлению кнопок, стрелок, точек  и стартовой страницы. `PaginationPageSettings`
 содержит настройки, относящиеся к управлению класса страницы, спиннера и анимации.  Все они передаются через **props** - `“:settings="settings”`. Массив **array_data** служит для вывода данных на страницу и  `является обязательным для заполнения`.

**Пример:**
```js
<template>
  <div id="app">
    <pagination-page :settings="settings">
      <div slot="page" slot-scope="item">
	  </div>
	</div>
    </pagination-page>
      <pagination-control :settings="settings" @callMethod="test"/>
      </div>
    </div>
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
            controlClass: '',
            controlStyle: '',
            maxButtons: 3,
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
          },
          arrowsSettings: {
            hideArrows: false,
            arrowStyle: '',
            arrowStyleColor: '',
            arrowStyleColorHover: ''
          },
          dotsSettings: {
            controlDotsStyle: '',
            controlDotsColor: ''
          },
          pageStarted: 1
          },
        PaginationPageSettings: {
          pageSettings: {
            pageClass: ''
          },
          spinnerSettings: {
            spinner: true,
            spinnerStyle: '',
            spinnerColor: ''
          },
          animationSettings: {
            animationPage: ''
          }
        }
      }
    }
  }
</script>
```
* Для вывода данных на страницу необходимо:

В массив `array_data` внести свои переменные (для вывода компонента переменной присваивается его название), затем в компоненте pagination-page записать их. Обращаемся к массиву элементов, указываем свойство originalEvent для вывода текущих данных и собственно саму переменную. Для вывода обычных данных используется `<div>`, а для компонентов - `<component>`. Строка `<div slot="page" slot-scope="item"></div>` является обязательной.
**Пример:**
```
array_data: [
  {
    data: 'apple',
    components: 'test1'
  }
]
```
```
<pagination-page :settings="settings">
  <div slot="page" slot-scope="item">
    <div >{{item.originalEvent.data}}</div>
    <components :is="item.originalEvent.components"></components>
  </div>
</pagination-page>
```
* Для вывода кнопок пагинации вставляем в шаблон компонент `pagination-control`.
**Пример:**
```
<pagination-control :settings="settings">
</pagination-control>
```
## Props
Имя | Тип | Все значения | Значения по умолчанию| Описание
:---: | :---: | :---: |:---: | --- |
*`PaginationControlSettings:`* |
**Buttons settings:** |
 *controlClass*| String | - | - | Задает общий класс родительскому блоку с кнопками пагинации.
*controlStyle* | String | square, circle, default | default |Задает вид кнопкам пагинации.
*maxButtons* | Number | - | 5 |Задаёт максимальное количество кнопок пагинации на странице.
*allpageButtonsStyle* | String | background: '', borderColor: '', color: '', backgroundHover: '',  borderColorHover : '', colorHover: '', fontFamily: '' | background: ‘#fff’, borderColor: ‘#02C8F3’, color: '#02C8F3', backgroundHover: ‘#02C8F3’, borderColorHover : ‘#02C8F3’, colorHover: ‘#fff’, fontFamily: 'Avenir' | background - Задает задний фон кнопкам пагинации; borderColor - Задает цвет рамки кнопкам пагинации;  color - Задает цвет кнопкам пагинации; backgroundHover - Задает задний фон кнопкам пагинации при наведении;  borderColorHover - Задает цвет рамки кнопкам пагинации  при наведении; colorHover - Задает цвет кнопкам пагинации при наведении; fontFamily - Задает шрифт кнопкам.
*currentPageButtonStyle* | String | backgroundActive: '', borderColorActive: '', colorActive: '' | backgroundActive: '#02C8F3', borderColorActive: '#02C8F3', colorActive: '#fff'  | backgroundActive - Задает задний фон активной кнопке; borderColorActive - Задает цвет рамки активной кнопке; colorActive - Задает цвет активной кнопке.
**Arrows settings:**|
 *hideArrows* | Boolean | true, false | false | Показывает либо скрывает стрелки пагинации.
*arrowStyle* | String | styleArrow-1, styleArrow-2, styleArrow-3 | styleArrow-2 | Меняет вид стрелок.
*arrowStyleColor* | String | - | #02C8F3 | Задает цвет стрелкам.
*arrowStyleColorHover* | String | - | #fff | Задает цвет стрелкам при наведении.
**Dots settings:** |
*controlDotsStyle* | String | styleDots-1, styleDots-2, styleDots-3 | styleDots-1 | Меняет вид многоточия.
*controlDotsColor* | String | - | #02C8F3 | Задает цвет многоточия.
**pageStarted:** | Number | - | 1 | Задает стартовую страницу.
*`PaginationPageSettings:`* |
**Page settings:** |
*pageClass* | String | - | - | Задает общий класс страницам.
**Spinner settings:** |
 *spinner* | Boolean | true, false | false | Показывает либо скрывает спиннер во время загрузки страницы.
*spinnerStyle* | String | spinnerStyle-1, spinnerStyle-2, spinnerStyle-3 | spinnerStyle-3 | Меняет вид спиннера.
*spinnerColor*| String | - | #fff | Задает цвет спиннера.
**Animations settings:** |
*animationPage* | String | fade, slide, bounce, default | default | Меняет вид анимации.
## Method
> Для вызова собственного метода, при переключении страниц, в компоненте `<pagination-control/>` в action callMethod нужно передать пользовательскую функцию, которая объявляется в объекте methods.

**Пример:**
```
<pagination-control @callMethod =" test "/>
```
```
methody: {
  test: function (e) {
    console.log (e)
  }
}
```
### Совместимость с браузером
Vue-smart-pagination успешно протестирован в браузерах таких как:
*  Chrome (66.0)
*  Safari (11.1)
*  Opera (52.0)
*  Firefox (59.0.2)
*  Edge (38.14393.0.0)

## Лицензия
LLC WebFriends. 2018

## Demo
![img](https://github.com/grinmax/vue-smart-pagination/raw/master/src/assets/demo.jpg)

