<template>
  <div class="page-container md-layout-column">
    <md-toolbar class="md-primary">
      
      <span class="md-title">My Title</span>

      <div class="md-toolbar-section-end">
        <md-button @click="showSidepanel = true">Favorites</md-button>
      </div>
    </md-toolbar>

    <md-drawer class="md-right" :md-active.sync="showSidepanel">
      <md-toolbar class="md-transparent" md-elevation="0">
        <span class="md-title">Favorites</span>
      </md-toolbar>

      <md-list>
        <md-list-item>
          <span class="md-list-item-text">Abbey Christansen</span>

          <md-button class="md-icon-button md-list-action">
            <md-icon class="md-primary">chat_bubble</md-icon>
          </md-button>
        </md-list-item>

      </md-list>
    </md-drawer>

    <md-content>
      <comics></comics>
    </md-content>
  </div>
</template>

<script>
    import Comics from './Comics'
    export default {
    name: 'navbar',
    data: () => ({
      showNavigation: false,
      showSidepanel: false
    }),
    components: {
        Comics
    }
  }
</script>

<style  scoped>
   .page-container {
    min-height: 300px;
    overflow: hidden;
    position: relative;
    border: 1px solid rgba(#000, .12);
  }

  .md-drawer {
    width: 230px;
    max-width: calc(100vw - 125px);
  }

  .md-content {
    padding: 16px;
  }
 
</style>