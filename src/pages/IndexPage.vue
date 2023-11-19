<template>
  <q-page class="q-pa-md">
    <div class="row">
      <div class="col-12 col-md-3 q-pa-xs" v-for="pokemon in pokemons" :key="pokemon.id">
        <q-card
          :class="pokemon.types[0].type.name=='grass' ? 'bg-green-8'
          : pokemon.types[0].type.name=='fire' ? 'bg-red-8'
          : pokemon.types[0].type.name=='water' ? 'bg-blue-8'
          : pokemon.types[0].type.name=='electric' ? 'bg-yellow-8'
          : pokemon.types[0].type.name=='poison' ? 'bg-deep-purple-8'
          : pokemon.types[0].type.name=='bug' ? 'bg-lime-8'
          : pokemon.types[0].type.name=='flying' ? 'bg-cyan-8'
          : pokemon.types[0].type.name=='normal' ? 'bg-grey-8'
          : pokemon.types[0].type.name=='ground' ? 'bg-brown-8'
          : pokemon.types[0].type.name=='fairy' ? 'bg-pink-8'
          : pokemon.types[0].type.name=='fighting' ? 'bg-deep-orange-8'
          : pokemon.types[0].type.name=='psychic' ? 'bg-purple-8'
          : pokemon.types[0].type.name=='rock' ? 'bg-orange-8'
          : pokemon.types[0].type.name=='steel' ? 'bg-blue-grey-8'
          : pokemon.types[0].type.name=='ice' ? 'bg-teal-8'
          : pokemon.types[0].type.name=='ghost' ? 'bg-indigo-8'
          : 'bg-grey-8'"
        >
          <q-card-section class="q-ma-md">
            <div class="row">
              <div class="col-6">
                <div class="text-capitalize text-white text-h6">{{pokemon.name}}</div>
                <q-chip dense v-for="type in pokemon.types" :key="type.type.name" :label="type.type.name" />
              </div>
              <div class="col-6">
                <q-img :src="'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/'+pokemon.id+'.png'" />
              </div>
            </div>
          </q-card-section>
        </q-card>
      </div>
    </div>
<!--    <pre>{{pokemons}}</pre>-->
  </q-page>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'IndexPage',
  data() {
    return {
      pokemons : []
    }
  },
  mounted() {
    this.getPokemon()
  },
  methods: {
    getPokemon() {
      for(let i = 1; i <= 151; i++) {
        this.$api.get('https://pokeapi.co/api/v2/pokemon-form/'+i).then(async res => {
          // console.log(res.data);
          await this.pokemons.push({
            id: i,
            name: res.data.name,
            image: res.data.sprites.front_default,
            types: res.data.types
          })
        });
      }
    }
  }
})
</script>
