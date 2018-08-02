<template>
    <div class="comics">
        <h1>Comics</h1>
            <div class="carrinho">
                <span v-if="carrinho.length == 0">Carrinho Vazio</span>
                <span v-else v-for="item in carrinho">
                    {{item.title}} : {{item.qntd}}<br>
                </span>
            </div>
            <div v-for="comic in comics">
                <md-card md-with-hover>
                    <md-ripple>
                        <md-card-header>
                          <div class="md-title">{{comic.title}}</div>
                          <div class="md-subhead">{{comic.resourceURI}}</div>
                        </md-card-header>
            
                        <md-card-content>
                          {{comic.format}}
                        </md-card-content>
            
                        <md-card-actions>
                          <md-button v-on:click="addComic(comic)">Action</md-button>
                        </md-card-actions>
                    </md-ripple>
                </md-card>
            </div>
            
            <!--https://jsonplaceholder.typicode.com/users
            https://www.youtube.com/watch?v=z6hQqgvGI4Y
            53:45
            -->

    </div>
</template>

<script>
    export default{
        name: 'comics',
        data() {
            return {
                comics: [],
                carrinho: []
            }
        },
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
            },
        },
        created: function(){
            this.$http.get('https://gateway.marvel.com/v1/public/comics?ts=1&apikey=4007f76057e3d86cc24a29c011b602b6&hash=def3b12836eb0da8878505663bb7c54a')
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
    
    .md-card {
        margin: 4px;
        display: inline-block;
        vertical-align: top;
    }
  
  
  li{
      list-style: none;
  }
 
</style>