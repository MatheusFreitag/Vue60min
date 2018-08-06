<template>
    <div class="comics">
        <h1>Comics</h1>
        <modal ref="Modal"></modal>
        <div v-for="comic in comics">
            <md-card>
              <md-card-media-cover md-solid>
                <md-card-media md-ratio="1:1">
                  <img :src="comic.images[0].path + '/portrait_xlarge.' + comic.images[0].extension" alt="comic">
                </md-card-media>

                <md-card-area>
                  <md-card-header>
                    <span class="md-title">{{comic.title}}</span>
                    <span class="md-subhead">{{comic.format}}</span>
                  </md-card-header>
        
                  <md-card-actions>
                    <md-button v-on:click="makeModalAppear(comic)" class="md-icon-button">
                      <md-icon>search</md-icon>
                    </md-button>
        
                    <md-button v-on:click="addComic(comic)" class="md-icon-button">
                      <md-icon>add</md-icon>
                    </md-button>
                  </md-card-actions>
                </md-card-area>
              </md-card-media-cover>
            </md-card>
        </div>
    </div>
</template>

<script>
    import Modal from './Modal'
    export default{
        name: 'comics',
        data() {
            return {
                comics: [],
                carrinho: []
            }
        },
        components: {
            Modal
        },
        props: ['pressed'],
        methods: {
            addComic: function(comic){
                var found = false, index = 0;
                for(let i = 0; i < this.carrinho.length; i++) {
                    if (this.carrinho[i].title == comic.title) {
                        found = true;
                        index = i;
                        break;
                    }
                }
                if (found == true){
                    this.carrinho[index].qntd += 1;
                }
                else{
                    this.carrinho.push({
                        title: comic.title,
                        qntd: 1
                    }) 
                }
                this.$emit('atualizaCarrinho', this.carrinho);
                
            },
            makeModalAppear: function(comic){
                this.$refs.Modal.changeState(comic)
            }
        },
        created: function(){
            this.$http.get('https://gateway.marvel.com/v1/public/comics?hasDigitalIssue=true&ts=1&apikey=4007f76057e3d86cc24a29c011b602b6&hash=def3b12836eb0da8878505663bb7c54a')
            .then(function(response){
                this.comics = response.data.data.results
            })
        }
    }
</script>

<style scoped>
    .contacted{
        text-decoration: line-through;
    }
    
  
  li{
      list-style: none;
  }
  
  .md-card {
    width: 320px;
    margin: 4px;
    display: inline-block;
    vertical-align: top;
  }
 
</style>