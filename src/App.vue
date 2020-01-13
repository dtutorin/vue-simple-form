<template>
  <div id="app">
    <CampaignRules/>
  </div>
</template>

<script>
  import CampaignRules from './components/CampaignRules.vue'

  export default {
    name: 'app',
    components: {
      CampaignRules
    }
  }
</script>

<style lang="scss">
  @import '~normalize.css/normalize.css';
  @import '~nprogress/nprogress.css';
  @import './styles/style.scss';
  
</style>
