<template lang="pug">
  div(id="app")
    tabs-component
</template>

<script>
import TabsComponent from '@/components/TabsComponent'
export default {
  name: 'App',
  components: { TabsComponent }
}
</script>

<style lang="scss" scoped>
@import '~scss/application';

#app {
  max-width: $app-container-size;
  margin: 0 auto;
}
</style>
