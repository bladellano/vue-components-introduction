<template>
  <div class="row">
    <!-- coluna 1 -->
    <div class="col-8">
      <h2>Filmes</h2>

      <ul class="list-group list-group-flush">
        <FilmesListaIten
          v-for="filme in filmes"
          :key="filme.id"
          :filme="filme"
          :class="aplicarClasseAtivar(filme)"
          @selecionarFilme="filmeSelecionado = $event"
        />
      </ul>
    </div>

    <!-- coluna 2 -->
    <div class="col-4">
      <FilmesListaItenInfo
        v-if="!editar"
        :filme="filmeSelecionado"
        @editarFilme="editarFilme"
      />

      <FilmesListaItenEditar 
      v-else
      :filme="filmeSelecionado" />
    </div>
  </div>
</template>

<script>

import { eventBus } from "./../main";

import FilmesListaIten from "./FilmesListaIten.vue";
import FilmesListaItenInfo from "./FilmesListaItenInfo.vue";
import FilmesListaItenEditar from "./FilmesListaItenEditar.vue";

export default {
  components: {
    FilmesListaIten,
    FilmesListaItenInfo,
    FilmesListaItenEditar,
  },
  data() {
    return {
      filmes: [
        {
          id: 1,
          titulo: "Vingadores: Guerra Infinita",
          ano: 2018,
          diretor: "Stan Lee",
        },
        {
          id: 2,
          titulo: "Homem Formiga e a Vespa",
          ano: 2018,
          diretor: "Stan Lee",
        },
        { id: 3, titulo: "Pantera Negra", ano: 2018, diretor: "Stan Lee" },
        { id: 4, titulo: "Deadpool II", ano: 2018, diretor: "Stan Lee" },
      ],
      filmeSelecionado: undefined,
      editar: false,
    };
  },
  methods: {
    aplicarClasseAtivar(filmeInterado) {
      return {
        active:
          this.filmeSelecionado &&
          this.filmeSelecionado.id === filmeInterado.id,
      };
    },
    editarFilme(filme) {
      this.editar = true;
      this.filmeSelecionado = filme;
    },
    atualizarFilme(filmeAtualizado){
      const indice = this.filmes.findIndex(filme => filme.id === filmeAtualizado.id)
      this.filmes.splice(indice,1, filmeAtualizado)
      this.filmeSelecionado = undefined
      this.editar = false
    }
  },
  created(){
    eventBus.$on('selecionarFilme',(filmeSelecionado)=>{
      this.filmeSelecionado = filmeSelecionado
    })

    eventBus.$on('atualizarFilme', this.atualizarFilme)
  }
};
</script>
