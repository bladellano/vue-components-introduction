<template>
  <li class="list-group-item">
    <span> {{ filme.titulo }} | {{ filme.ano }} </span>
    <button @click="selecionar" class="btn btn-secondary float-right">
      Selecionar
    </button>
  </li>
</template>

<script>
import { eventBus } from "./../main";

export default {
  // props:['filmeTitulo'],
  // inheritAttrs:false,
  props: {
    filme: {
      type: Object,
      required: true,
    },
    // titulo:{
    //     type:String,
    //     required:true
    // },
    // ano:{
    //     type:Number,
    //     required:true
    // }
  },
  // computed:{
  //     filmeTituloConcatenado(){
  //         return `Título: ${this.titulo}`
  //     }
  // },
  methods: {
    selecionar() {
      // this.$emit('selecionarFilme',this.filme)
      // eventBus.$emit("selecionarFilme", this.filme);
      eventBus.selecionarFilme(this.filme);
    },
  },
  created() {
    // console.log('Filme Título:', this.titulo)
    // console.log(typeof this.titulo);
    // console.log('Attrs: ', this.$attrs)
  },
};
</script>
