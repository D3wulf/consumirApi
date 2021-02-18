<template>
  <Titulo texto="Blog" />
  <!--<button @click="consumirApi">Coger Api</button>-->

  <div v-for="datos in arrayBlog" :key="datos.id">
      <!--ojo que hay que poner :to porque es dinamico-->
      <router-link :to="`/blog/${datos.id}`">{{datos.title}}</router-link> 


  </div>
</template>

<script>
// @ is an alias to /src
import Titulo from '../components/Titulo'



export default {
  
  components: {
    Titulo
    
  },data(){

      return{

          arrayBlog:[]
      }
  },
  methods:{
      async consumirApi(){

          try{
              //coge los datos de la url
              const datos= await fetch('https://jsonplaceholder.typicode.com/posts')
              //metelos en json
              const datosConseguidos= await datos.json()
              //metemos en el array para poder acceder a los objetos del json
              this.arrayBlog = datosConseguidos;



          }catch(error){

              console.log(error);
          }
      }
  },
  //no usar funcion de flecha, necesitamos el this

  //cada vez que cargue la vista ejecutara la funcion
  created(){

      this.consumirApi();


  }
}
</script>
<style>

</style>