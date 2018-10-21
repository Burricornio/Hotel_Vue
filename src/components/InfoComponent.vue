<template lang="pug">
  article(class="info-container")

    div(class="row")
      img(class="info-container__img" :src="image")

      div(class="info-container__item")

        div(class="info-container__item__text")

          h2(class="info-container__item__text__title") {{ title }}

          div(class="info-container__item__text__body")
            p(v-for="paragraph in description" class="info-container__item__text__body__p") {{ paragraph }}

        span(class="info-container__item__info" @click="moreInfoAction($event)") Más información y condiciones

    div(class="row")
      div(class="info-container__more-info" :class="{ show: moreInfoSelected }")

        h3(class="info-container__more-info__title") Incluye

        ul(class="info-container__more-info__list")
          li(v-for="item in moreInfoItems" class="info-container__more-info__list__item") {{ item }}

        span(class="info-container__more-info__legend") Valores no acumulables a otras promociones similares

</template>

<script>
export default {
  name: 'InfoComponent',
  props: {
    title: {
      type: String,
      default: 'Insert title'
    },
    description: {
      type: Array,
      default: () => []
    },
    image: {
      type: String
    },
    moreInfoItems: {
      type: Array,
      default: () => []
    }
  },
  data () {
    return {
      moreInfoSelected: false
    }
  },
  methods: {
    // Funcionalidad que despliega el panel de mas opciones
    moreInfoAction (e) {
      // Toggle sobre la clase 'active' en el span
      e.target.classList.toggle('active')
      // Muestra u oculta panel
      this.moreInfoSelected = !this.moreInfoSelected
    }
  }
}
</script>

<style lang="scss" scoped>
  @import '~scss/application';

  .info-container {
    @include display-flex($direction: column);
    padding-bottom: 17px;
    margin-bottom: 21px;

    @include if-tablet-portrait {
      border: $info-border;
    }

    .row {
      //  @include display-flex($justify: flex-start);
       @include display-flex($justify: flex-start, $direction: column);
       width: 100%;

      @include if-tablet-portrait {
        flex-direction: row;
      }
    }

    &__img {
      display: flex;

      @include if-tablet-portrait {
        align-self: flex-start;
        padding-top: 0;
      }
    }

    &__item {
      @include display-flex($direction: column, $align: flex-start, $justify: space-between);
      padding: 18px 27px 0;
      align-self: stretch;

      &__text {

        &__title {
          font-family: $info-title-font-family;
          color: $info-title-color;
          margin: 0;
          font-size: 18px;
        }

        &__body {
          margin-top: 6px;
          color: $info-body-color;
          font-family: $info-body-font-family;
          font-size: 14px;

          @include if-tablet-portrait {
            // padding-right: 280px;
          }
        }
      }

      &__info {
        color: $info-info-color;
        font-family: $info-info-font-family;
        font-weight: 700;
        font-size: 14px;
        cursor: pointer;

        &::after {
          content: '';
          background-image: url('../assets/accordion-component/angle-down-blue.svg');
          width: 14px;
          height: 21px;
          display: block;
          float: right;
          margin-left: 14px;
          background-size: 14px 21px;
          transition: all .2s linear;
        }

        &.active::after {
          transform: rotate(-180deg) translateY(-7%);
        }
      }
    }

    &__more-info {
      width: 100%;
      font-family: $info-more-info-font-family;
      color: $info-more-info-color;
      font-size: 14px;
      padding-left: 55px;
      max-height: 0;
      transition: all .5s ease-in-out;
      opacity: 0;
      margin-top: 18px;

      @include if-tablet-portrait {
        // padding-left: 80px;
      }

      &.show {
        opacity: 1;
        max-height: 100%;
      }

      &__title {
        margin-top: 0;
        font-size: 16px;
        font-weight: 400;
      }

      &__list {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        padding: 0 40px 0 0;

        @include cards-styles {
          flex-direction: column;
          height: 120px;
        }

        &__item {
          margin-left: 20px;
          margin-top: 6px;

          @include cards-styles {
            width: 250px;
          }
        }
      }

      &__legend {
        font-weight: 700;
        font-size: 12px;
        color: $info-more-info-legend-color;

        @include if-tablet-portrait {
          font-size: 14px;
        }
      }
    }
  }
</style>
