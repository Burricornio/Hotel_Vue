<template lang="pug">
  article(class="news-container")
    img(class="news-container__img" src="../assets/img/yoga.png")
    div(class="news-container__item")
      h2(class="news-container__item__title") Olvídese de la rutina
      p(class="news-container__item__body") Cras vehicula vestibulum dapibus. Pellentesque auctor dolor et purus facilisis maximus. Mauris eget urna luctus, imperdiet neque nec, aliquet lorem.
</template>

<script>
export default {
  name: 'ArticleComponent'
}
</script>

<style lang="scss" scoped>
  @import '~scss/application';

  .news-container {
    @include display-flex;
    border: $news-border;

    &__img {
      display: block;
    }

    &__item {
      @include display-flex($direction: column, $align: flex-start);
      padding-left: 27px;
      align-self: flex-start;

      &__title {
        font-family: $news-title-font-family;
        color: $news-title-color;
        font-size: 18px;
      }

      &__body {
        color: $news-body-color;
        font-family: $news-body-font-family;
        font-size: 14px;
        padding-right: 280px;
      }
    }
  }
</style>
