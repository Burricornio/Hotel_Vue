<template lang="pug">

  article(class="card" :class="{ active: checked }")

    header(class="card__title")
      h3(class="card__title__text") {{ title }}
      div(class="card__title__line")

      ul(class="card__list")
        li(v-for="item in items" class="card__list__item")
          span(class="card__list__item__text")  {{ item }}

    div(class="card__action-container" :class="{ active: checked }" @click="isChecked")
      input(class="card__action-container__input" type="radio" :checked="checked")
      span(class="card__action-container__custom-input")
      | Elegir régimen

</template>

<script>
export default {
  name: 'CardComponent',
  props: {
    title: {
      type: String,
      default: 'Insert card title'
    },
    items: {
      type: Array,
      default: () => ['Sin régimen', 'Botella de agua de bienvenida']
    }
  },
  data () {
    return {
      checked: false
    }
  },
  methods: {
    // Función para activar botón
    isChecked () {
      this.checked = !this.checked
    }
  }
}
</script>

<style lang="scss" scoped>
  @import '~scss/application';

  .card {
    @include display-flex($justify: space-between, $direction: column);
    background: $card-color;
    width: $card-max-width;
    max-width: $card-max-width;
    border: 1px solid $card-border-color;
    font-family: $card-font-family;
    min-height: $card-min-height;

    ~ .card {
      margin-left: $card-margin-left;
    }

    &.active {
      border: 1px solid $card-border-color-active;
      transition: border .2s linear;
    }

    &__title {
      @include display-flex($direction: column);

      &__text {
        @include display-flex($direction: column);
        text-align: center;
        color: $card-title-color;
        font-size: 16px;
        font-weight: 700;
        padding: 0 30px;
        min-height: 40px;
        margin: 16px 0;
      }

      &__line {
        width: 70px;
        border-bottom: 1px solid $blue-03;
      }
    }

    &__list {
      font-size: 15px;

      &__item {
        color: $card-list-circle-color;
        margin-bottom: 6px;

        &__text {
          color: $card-list-text-color;
        }
      }
    }

    &__action-container {
      @include display-flex;
      background-color: $card-button-color;
      color: $card-button-text-color;
      margin: 0 16px 18px;
      font-size: 16px;
      padding: 15px 25px;
      border: 1px solid $white-01;
      transition: border .2s linear;
      cursor: pointer;

      &.active {
        border: 1px solid $card-border-color-active;
        transition: border .2s linear;
      }

      &__input {
        display: none;

       &:checked ~ .card__action-container__custom-input {
          border-color: $card-input-color;

          &::after {
              display: block;
              opacity: 1;
          }
        }
      }

      &__custom-input {
          height: 16px;
          width: 16px;
          border: 1px solid $card-input-border-color;
          border-radius: 50%;
          margin-right: 13px;

          &::after {
            content: "";
            display: none;
            opacity: 0;
            animation-name: fadeIn; animation-duration: .2s; animation-timing-function: linear;
            top: 50%;
            left: 50%;;
            width: 10px;
            height: 10px;
            border-radius: 50%;
            transform: translate(calc(50% - 2px), calc(50% - 2px));
            background: $green-01;
          }
      }
    }
  }

@keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
</style>
