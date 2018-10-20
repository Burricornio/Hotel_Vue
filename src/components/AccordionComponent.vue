<template lang="pug">
  div(class="accordion-container")
    button(class="accordion-container__btn" @click="accordionAction($event)") {{ title }}
    div(class="accordion-container__content")
      slot
</template>

<script>
export default {
  name: 'AccordionComponent',
  props: {
    title: {
      type: String,
      default: 'Insert Accordion Title'
    }
  },
  methods: {
    // Funcionalidad click acordeón
    accordionAction (e) {
      // Toggle sobre la clase 'active' en el botón
      e.target.classList.toggle('active')
      // Toggle sobre el panel con la clase 'show'
      e.target.nextSibling.classList.toggle('show')
    }
  }
}
</script>

<style lang="scss" scoped>
  @import '~scss/application';

  .accordion-container {
    border: $accordion-border;
    padding: 0 30px;

    &__btn {
      background-color: $accordion-bgcolor;
      width: 100%;
      height: $accordion-height;
      font-family: $accordion-font-family-title;
      color: $accordion-title-color;
      font-size: 24px;
      font-weight: 700;
      line-height: 38px;
      cursor: pointer;
      border: none;
      text-align: left;
      outline: none;
      transition: 0.4s;
      padding: 0;

      &::before {
        content: url('../assets/accordion-component/angle-down-blue.svg');
        margin-right: 20px;
        transition: all .2s linear;
      }

      &::after {
        content: 'Opcional';
        font-family: $accordion-font-family-title-optional;
        color: $accordion-title-optional-color;
        font-weight: 400;
        font-size: 12px;
        margin-left: 18px;
        transition: all .2s linear;
      }

      &.active::before {
        content: url('../assets/accordion-component/angle-down-blue.svg');
        transform: rotate(-180deg) translateY(19%);
      }
    }

    &__content {
      background-color: white;
      max-height: 0;
      overflow: hidden;
      transition: 0.6s ease-in-out;
      opacity: 0;

      &.show {
        opacity: 1;
        max-height: 500px;
      }
    }
  }
</style>
