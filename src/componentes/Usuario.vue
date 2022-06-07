<template>
  <section class="src-componentes-usuario">
    <div class="jumbotron">
      <h2>Usuarios</h2>
      <hr>
      <hr>
      <br>

      <button class="btn btn-success my-3 mr-3" @click="getUsuariosAxios()">Pedir Usuarios Axios</button>
      <button class="btn btn-success my-3 mr-3" @click="getUsuariosFetch()">Pedir Usuarios Fetch </button>
      <button class="btn btn-danger my-3" @click="usuarios=[]">LIMPIAR</button>
      <br>

      <div v-if="usuarios.length" class="table-responsive">
        <table class="table table-dark">
          <tr>
            <th>Id</th>
            <th>Nombre</th>
            <th>Email</th>
            <th>Telefono</th>
          </tr>
          <tr v-for="(usuario, index) in usuarios" :key="index">
              <td>{{ usuario.id}}</td>
              <td>{{ usuario.nombre }}</td>
              <td>{{ usuario.email }}</td>
              <td>{{ usuario.telefono }}</td>
          </tr>
        </table>
        <h5 class="alert alert-primary">Se encontraron {{usuarios.length}} usuarios.</h5>
      </div>
      <h4 v-else class="alert alert-danger text-center">No se encontraron Usuarios</h4>

     </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-componentes-usuario',
    props: [],
    mounted () {

    },
    data () {
      return {
        url: 'https://629f50a48b939d3dc294f550.mockapi.io/usuarios',
        usuarios: []
      }
    },
    methods: {
      async getUsuariosFetch(){
        try {
          let response = await fetch(this.url)
          let respuesta = await response.json()
          this.usuarios = respuesta
        }
        catch(error){
          console.error('Error Fetch', error)
        }

      },
      async getUsuariosAxios() {
        try{
          let { data } = await this.axios(this.url)
          this.usuarios = data
        }
        catch(error){
          console.error('Error Axios', error)
        }
      }

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .src-componentes-usuario {

  }

  .jumbotron {
    background-color: rgb(5, 24, 25);
    color: white;
  }

  hr {
    background-color: #bbb;
  }  
</style>
