<template>
  <Titulo texto="Ruta con parámtros"/>
  <h2>Parametro: {{ $route.params.id }}</h2>
  <h3>{{ articulo.title }}</h3>
  <p>{{ articulo.id }} - {{ articulo.body }}</p>
</template>
<script>
import Titulo from '../components/Titulo'
export default {
  components: {
    Titulo
  },
  data(){

    return {
      articulo:{}
    }
  },
  methods: {
    async consumirArticulo(){
        try{
          //queremos acceder al objeto y para ello cogemos la id que tenemos en el template
          //vamos a coger esa cata, la transformamos a json y la metemos en el objeto
          const data = await fetch(`https://jsonplaceholder.typicode.com/posts/${this.$route.params.id}`)
          const objeto = await data.json()
          this.articulo = objeto

        }catch(error){
          console.log(error)
        }
    }
  },
  created(){
        this.consumirArticulo()
    }
}
</script>