<template>
    <!-- TEMPLATE DISPONIVEL NO BULMA -->
    <div>
        <div class="card">
        <div class="card-image">
            <figure >
            <img :src="currentImg" alt="Placeholder image">
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
            <div class="media-content">
                <p class="title is-4">{{num + 1}} - {{upper(name)}}</p>
                <p class="subtitle is-6">{{pokemon.type }}</p>
            </div>
            </div>

            <div class="content">
                <button class="button is-info is-outlined" @click="changeSize">Change Size</button>
            </div>
        </div>
        </div>
    </div>
      
</template>

<script>
// axios para consumir API
import axios from 'axios';


export default {
    // pegando detalhes de cada pokemon a partir de sua URL
   created: function(){
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name
            this.pokemon.front = res.data.sprites.front_default
            this.pokemon.back = res.data.sprites.back_default
            this.currentImg = this.pokemon.front

        }).catch(err => {
            console.log(err)
        });
   },
   data(){
    return {
        pokemon: {},
        isFront: true,
        currentImg: ''
    }
   },
    props: {
        name: String,
        num: Number,
        url: String
    },
    // metodo/filtro para deixar letra maiuscula no nome
    methods: {
        upper: function(value){
            var newName = value[0].toUpperCase() + value.slice(1)
            return newName
        },
        // metodo para mudar a imagem do pokemon
        changeSize: function(){
            if(this.isFront){
                this.isFront = false
                this.currentImg = this.pokemon.back
            }else {
                this.isFront = true
                this.currentImg = this.pokemon.front
            }
        }
    }
};
</script>

<style scoped>

</style>