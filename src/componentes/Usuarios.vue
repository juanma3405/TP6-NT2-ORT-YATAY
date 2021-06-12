<template>
  <section class="src-componentes-usuarios">
    <div class="jumbotron">
      <h1>Usuarios</h1>
      <hr />
      <br />

      <!--  <pre>{{ usuarios }}</pre> -->

      <div class="alert alert-info">
        <div v-if="usuarios.length">
          <div
            class="media alert alert-warning"
            v-for="(usuario, index) in usuarios"
            :key="index"
          >
            <div class="media-body ml-3">
              <h5>
                <u>Usuario {{ index + 1 }}</u>
              </h5>
              <br />
              <p>Usuario: {{ usuario.nombre }}</p>
              <p>Edad: {{ usuario.edad }}</p>
              <p>Email: {{ usuario.email }}</p>
            </div>
          </div>
        </div>
        <h2 v-else class="alert alert-warning">
          no se encontraron usuarios disponibles
        </h2>
      </div>
    </div>
  </section>
</template>

<script lang="js">

  export default  {
    name: 'src-componentes-usuarios',
    props: [],
    mounted () {
      this.getUsuariosAxiosAsyncAwait()
    },
    data () {
      return {
        url: 'https://60a96f6d20a641001730725a.mockapi.io/usuarios',
        usuarios: []
      }
    },
    methods: {    
      getUsuariosAxios() {
          this.axios(this.url)
          .then( respuesta => {
          console.log('AXIOS GET USUARIOS', respuesta.data)
          this.usuarios = respuesta.data
          })
          .catch(error => console.error(error))
        },

       async getUsuariosAxiosAsyncAwait() {
        try {
          let respuesta = await this.axios(this.url)
          console.log('AXIOS GET USUARIOS', respuesta.data)
          this.usuarios = respuesta.data
        }
        catch(error) {
          console.error(error)
        } 
      }
    },
    computed: {
    
    }
}


</script>

<style scoped lang="css">
.src-componentes-usuarios {
}

.jumbotron {
  background-color: white;
  color: darkblue;
}
</style>
