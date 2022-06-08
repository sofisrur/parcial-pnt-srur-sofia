<template>

  <section class="src-componentes-respuestas">
    <div class="jumbotron">
   <h2>RESPUESTAS</h2>
      <hr>
      <br>

      <div class="table-responsive">
        <table class="table table-dark">
          <tr>
            <th>Numero de pregunta</th>
            <th>Respuesta</th>
          </tr>
          <tr v-for="(pregunta, index) in preguntas" :key="index">
            <td>{{pregunta.numero}}</td>
            <td>{{pregunta.respuestas}}</td>
          </tr>
        </table>
      </div>      

    </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-componentes-respuestas',
    props: [],
    mounted () {

    },
    data () {
      return {
          preguntas : [ 
            { numero: 1, respuestas: ['C','D'] },
            { numero: 2, respuestas: ['C'] },
            { numero: 3, respuestas: ['B'] }
          ]
      }
    },
    methods: {

    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .jumbotron {
    background: rgb(210, 93, 93);
    color: #333;
  }

  hr {
    background-color: #eee;
  }
</style>