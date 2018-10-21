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
        title="Mejora tu estancia"
      )
        info-component(
          title="Olvídese de la rutina",
          :image="require('../assets/img/yoga.png')"
          :description="['Cras vehicula vestibulum dapibus. Pellentesque auctor dolor et purus facilisis maximus. Mauris eget urna luctus, imperdiet neque nec, aliquet lorem.']"
          :more-info-items="['Baño javanés Mandi Susu tradicional: evocación de los baños que tomaban las princesas de las cortes y palacios de Java Central, en Indonesia, con antiguas recetas en las que se mezclaba la leche y las especias.', 'Baño floral balinés: con aceite de almendra dulce y aromas de jazmín.', 'Baño oceánico: con sal marina y gajos de mandarina o lima.', 'Baño de pies floral: baño aromático de pies, con pétalos y aromas.', 'Baño de vapor herbal: baño de vapor con hierbas del sudeste asiático.', 'Rain shower.']"
        )

      accordion-component(
        title="Servicios de habitación"
      )
        info-component(
          title="Experiencias y programas SPA con agua",
          :image="require('../assets/img/spa.png')"
          :description="['Las experiencias spa de agua tienen una presencia muy especial en SPA Sensations. No es extraño si consideramos que la mayor parte del planeta, así como del propio cuerpo humano, están compuestos de agua.', 'El arte de recrear experiencias de agua en variaciones ilimitadas es la base de la propuesta de SPA Sensations a sus clientes, aportando el refinamiento al baño y a la hidratación en todas sus formas. Un mundo mágico de posibilidades, más allá de la terapia y del que ahora usted, también podrá disfrutar.']"
          :more-info-items="['Baño javanés Mandi Susu tradicional: evocación de los baños que tomaban las princesas de las cortes y palacios de Java Central, en Indonesia, con antiguas recetas en las que se mezclaba la leche y las especias.', 'Baño floral balinés: con aceite de almendra dulce y aromas de jazmín.', 'Baño oceánico: con sal marina y gajos de mandarina o lima.', 'Baño de pies floral: baño aromático de pies, con pétalos y aromas.', 'Baño de vapor herbal: baño de vapor con hierbas del sudeste asiático.', 'Rain shower.']"
        )

</template>

<script>
// Imports de componentes
import AccordionComponent from '@/components/AccordionComponent'
import CardComponent from '@/components/CardComponent'
import InfoComponent from '@/components/InfoComponent'

export default {
  name: 'TabsComponent',
  components: { AccordionComponent, CardComponent, InfoComponent },
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
        width: 50%;
        text-align: center;

        @include if-tablet-portrait {
          width: auto;
        }

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
        @include display-flex($direction: column);
        color: $blue-01;
        font-size: $tabs-title-font-size;
        text-align: center;
        font-family: $secondary-font-family;

        @include if-tablet-portrait {
          flex-direction: row;
        }

        &__category {
          font-weight: 400;
          color: $blue-01;
          margin-right: 8px;
        }

        &__name {
          font-weight: 700;
          font-size: $tabs-title-font-size;
          margin: 0;
          padding: 0 20px;
        }

        &__stars {
          margin-left: 20px;

          &__star {
            margin: 0 5px;
          }
        }
      }

      &__cards-container {
        @include display-flex($direction: column);

        @include if-tablet-portrait {
          flex-direction: row;
          flex-wrap: wrap;
          margin-top: 10px;
        }
      }
    }
  }

  // Animaciones
  @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
  @keyframes appear { from { transform: translateX(-100%); opacity: 0; } to { transform: translateX(0%); opacity: 1; } }

</style>
