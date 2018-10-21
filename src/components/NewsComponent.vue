<template lang="pug">
  article(class="news-container")

    div(class="row")
      img(class="news-container__img" src="../assets/img/yoga.png")

      div(class="news-container__item")

        div(class="news-container__item__text")

          h2(class="news-container__item__text__title") Olvídese de la rutina

          div(class="news-container__item__text__body")
            p(class="news-container__item__text__body__p") Las experiencias spa de agua tienen una presencia muy especial en SPA Sensations. No es extraño si consideramos que la mayor parte del planeta, así como del propio cuerpo humano, están compuestos de agua.
            p(class="news-container__item__text__body__p") El arte de recrear experiencias de agua en variaciones ilimitadas es la base de la propuesta de SPA Sensations a sus clientes, aportando el refinamiento al baño y a la hidratación en todas sus formas. Un mundo mágico de posibilidades, más allá de la terapia y del que ahora usted, también podrá disfrutar.

        span(class="news-container__item__info" @click="moreInfoAction($event)") Más información y condiciones

    div(class="row")
      div(class="news-container__more-info" :class="{ show: moreInfoSelected }")

        h3(class="news-container__more-info__title") Incluye

        ul(class="news-container__more-info__list")
          li(class="news-container__more-info__list__item") Baño javanés Mandi Susu tradicional: evocación de los baños que tomaban las princesas de las cortes y palacios de Java Central, en Indonesia, con antiguas recetas en las que se mezclaba la leche y las especias.
          li(class="news-container__more-info__list__item") Baño floral balinés: con aceite de almendra dulce y aromas de jazmín.
          li(class="news-container__more-info__list__item") Baño oceánico: con sal marina y gajos de mandarina o lima.
          li(class="news-container__more-info__list__item") Baño de pies floral: baño aromático de pies, con pétalos y aromas.
          li(class="news-container__more-info__list__item") Baño de vapor herbal: baño de vapor con hierbas del sudeste asiático.
          li(class="news-container__more-info__list__item") Rain shower.

        span(class="news-container__more-info__legend") Valores no acumulables a otras promociones similares

</template>

<script>
export default {
  name: 'ArticleComponent',
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

  .news-container {
    @include display-flex($direction: column);
    border: $news-border;
    padding-bottom: 17px;
    margin-bottom: 21px;

    .row {
       @include display-flex($justify: flex-start);
       width: 100%;
    }

    &__img {
      display: flex;
      align-self: flex-start;
    }

    &__item {
      @include display-flex($direction: column, $align: flex-start, $justify: space-between);
      padding: 18px 27px;
      align-self: stretch;

      &__text {

        &__title {
          font-family: $news-title-font-family;
          color: $news-title-color;
          margin: 0;
          font-size: 18px;
        }

        &__body {
          margin-top: 6px;
          color: $news-body-color;
          font-family: $news-body-font-family;
          font-size: 14px;
          padding-right: 280px;
        }
      }

      &__info {
        color: $news-info-color;
        font-family: $news-info-font-family;
        font-weight: 700;
        font-size: 14px;

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
      font-family: $news-more-info-font-family;
      color: $news-more-info-color;
      font-size: 14px;
      padding-left: 80px;
      max-height: 0;
      transition: all .5s ease-in-out;
      opacity: 0;

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
        flex-direction: column;
        flex-wrap: wrap;
        height: 120px;
        padding: 0;

        &__item {
          width: 250px;
          margin-left: 20px;
        }
      }

      &__legend {
        font-weight: 700;
        color: $news-more-info-legend-color;
      }
    }
  }
</style>
