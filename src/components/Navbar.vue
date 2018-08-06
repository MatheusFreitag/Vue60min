<template>
  <div class="page-container md-layout-column" >
    <md-toolbar class="md-primary">
      
      <span class="md-title">Comic Store</span>

      <div class="md-toolbar-section-end">
        <md-button @click="showSidepanel = true">Carrinho <span class="numItems">{{numItems}}</span></md-button>
      </div>
    </md-toolbar>

    <md-drawer class="md-right" :md-active.sync="showSidepanel">
      <md-toolbar class="md-transparent" md-elevation="0">
        <span class="md-title">Carrinho</span>
      </md-toolbar>

      <md-list>
        <span v-for="item in carrinho"  v-bind:key="item.title">
          <md-list-item>
            <span>{{item.title}}</span>
            <span class="qntd">{{item.qntd}}</span>
          </md-list-item>
          <hr>
        </span>

      </md-list>
    </md-drawer>

    <md-content>
      <comics v-on:atualizaCarrinho="trocaCarrinho"></comics>
    </md-content>
  </div>
</template>

<script>
    import Comics from './Comics'
    export default {
    name: 'navbar',
    data: () => ({
      showNavigation: false,
      showSidepanel: false,
      menuVisible: false,
      carrinho: [],
      numItems: 0
    }),
    components: {
        Comics
    },
    methods :{
      trocaCarrinho: function(novoCarrinho){
        this.carrinho = novoCarrinho;
        this.numItems += 1;
      }
    },
    created: ()=>{
      this.carrinho = []
    }
  }
</script>

<style lang="scss" scoped>
  .page-container {
    min-height: 300px;
    overflow: hidden;
    position: relative;
    border: 1px solid rgba(#000, .12);
  }

  .md-drawer {
    width: 630px;
    max-width: calc(100vw - 635px);
  }

  .md-content {
    padding: 16px;
  }
  
  .qntd{
    background: pink;
    padding: 5px 11px;
    border-radius: 50%;
  }
  
  .numItems{
    background: white;
    padding: 5px 9px;
    border-radius: 50%;
    color: gray;
  }
  
  hr{
    width: 90%;
    opacity: .2;
  }
</style>