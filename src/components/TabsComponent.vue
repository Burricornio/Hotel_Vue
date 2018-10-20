<template lang="pug">
  div(class="tabs-container")

    div(class="tabs-container__tabs")

      div(
        class="tabs-container__tabs__item active"
        @click="changeTab($event, 'tab1')"
        ref="button1") Tab 1

      div(
        class="tabs-container__tabs__item"
        @click="changeTab($event, 'tab2')"
        ref="button2") Tab 2

    //- Tab 1
    section(class='tabs-container__content active' ref="tab1")

      div(class="tabs-container__content__title")

        span(class="tabs-container__content__title__category") HOTEL

        h2(class="tabs-container__content__title__name") Mieres del Camín Apartamentos

        div(class="tabs-container__content__title__stars")

          img(class="tabs-container__content__title__stars__star" src="@/assets/tabs-component/star-orange.svg" alt="Orange start")
          img(class="tabs-container__content__title__stars__star" src="@/assets/tabs-component/star-orange.svg" alt="Orange start")
          img(class="tabs-container__content__title__stars__star" src="@/assets/tabs-component/star-orange.svg" alt="Orange start")
          img(class="tabs-container__content__title__stars__star" src="@/assets/tabs-component/star-orange.svg" alt="Orange start")

      div(class="tabs-container__content__cards-container")

        card-component(
          title="Solo alojamiento"
          :items="['Sin régimen', 'Botella de agua de bienvenida']"
        )

        card-component(
          title="Alojamiento y Desayuno"
          :items="['Desayuno buffet completo']"
        )

        card-component(
          title="Media Pensión"
          :items="['Desayuno buffet completo', 'Cena buffet', 'No incluye']"
        )

        card-component(
          title="Todo incluido"
          :items="['Dispondrás de comida y bebida todo el día y durante toda tu estancia', 'Restaurante buffet', 'Snack bar', 'Servicio de bares (marcas nacionales)']"
        )

        card-component(
          title="Unlimited Services"
          :items="['Restaurante buffet con bebidas Premium', 'Restaurante a la carta (una cena por estancia)', 'Snack Bar con bebidas Premium', 'Minibar incluido', 'Acceso a SPA y 45 minutos de masaje por persona', 'Actividades deportivas (acuáticas sin motor)', 'Caja fuerte', 'Parking gratuito', 'Lavandería']"
        )

    //- Tab 2
    section(class='tabs-container__content' ref="tab2")

      accordion-component(
        title="Servicios de habitación"
      )
        news-component

</template>

<script>
// Imports de componentes
import AccordionComponent from '@/components/AccordionComponent'
import CardComponent from '@/components/CardComponent'
import NewsComponent from '@/components/NewsComponent'

export default {
  name: 'TabsComponent',
  components: { AccordionComponent, CardComponent, NewsComponent },
  methods: {
    // Metodo para desplazarse entre las tabs
    changeTab (e, tab) {
      // Elimina clase activa tanto del contenido y de las tabs
      Object.keys(this.$refs).forEach(element => this.$refs[element].classList.remove('active'))
      // Añade la clase activa a la tab seleccionada
      e.target.classList.add('active')
      // Añade la clase active al item seleccionado
      this.$refs[tab].classList.add('active')
    }
  }
}
</script>

<style lang="scss" scoped>
  @import '~scss/application';

  .tabs-container {
    @include display-flex($direction: column);
    overflow: hidden;
    background: $tabs-bgcolor-color;
    font-family: $tabs-font-family;

    &__tabs {
      @include display-flex($justify: flex-end);
      width: 100%;
      box-shadow: $tabs-box-shadow;
      z-index: 2;

      &__item {
        box-sizing: border-box;
        height: $tabs-height;
        line-height: $tabs-height;
        padding: 0 30px;
        cursor: pointer;
        color: $tabs-color;
        transition: color .3s linear;
        border-bottom: 2px solid $white-01;

        &:hover {
          border-bottom: 2px solid $tabs-color;
        }

        &.active {
          box-sizing: border-box;
          outline: none;
          color: $tabs-active-color;
          border-bottom: 2px solid $tabs-active-color;
        }
      }
    }

    &__content {
      width: 100%;
      background: $tabs-content-color;
      display: none;
      padding-top: 40px;

      &.active {
        display: block;
        animation-name: appear; animation-duration: .4s; animation-timing-function: linear;
      }

      &__title {
        @include display-flex;
        color: $blue-01;
        font-size: $tabs-title-font-size;
        text-align: center;
        font-family: $secondary-font-family;

        &__category {
          font-weight: 400;
          color: $blue-01;
          margin-right: 8px;
        }

        &__name {
          font-weight: 700;
          font-size: $tabs-title-font-size;
        }

        &__stars {
          margin-left: 20px;

          &__star {
            margin: 0 5px;
          }
        }
      }

      &__cards-container {
        @include display-flex;
      }
    }
  }

  // Animaciones
  @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
  @keyframes appear { from { transform: translateX(-100%); opacity: 0; } to { transform: translateX(0%); opacity: 1; } }

</style>
