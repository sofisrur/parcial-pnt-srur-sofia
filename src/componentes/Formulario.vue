<template>

  <section class="src-componentes-formulario">
    <div class="jumbotron">
      <h2>INGRESO NOTAS</h2>
      <hr>
     <vue-form :state="formstate" @submit.prevent="enviar()">
        
        <validate tag="div">
          <label for="nombre">Ingrese el nombre:</label>
          <input 
          type="text" 
          id="nombre" 
          v-model.trim="formData.nombre" 
          required 
          :minlength="caracterMinimo" 
          :maxlength="caracterMaximo" 
          no-espacios 
          name="nombre" 
          autocomplete="off" 
          class="form-control" />
    
          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio</div>
            <div slot="minlength" class="alert alert-danger mt-1">Este campo debe poseer al menos {{caracterMinimo}} caracteres</div>
            <div v-if="formData.nombre && (formData.nombre.length == 15)" class="alert alert-danger mt-1">Este campo debe poseer como máximo {{caracterMaximo}} caracteres</div>
            <div slot="no-espacios" class="alert alert-danger mt-1">Este campo no permite espacios intermedios</div>
          </field-messages>
        </validate>
        <br>

        <validate tag="div">
          <label for="apellido">Ingrese el apellido:</label>
          <input 
          type="text" 
          id="apellido" 
          v-model="formData.apellido" 
          required 
          :minlength="caracterMinimo" 
          :maxlength="caracterMaximo" 
          no-espacios 
          name="apellido" 
          autocomplete="off" 
          class="form-control" />
    
          <field-messages name="apellido" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio</div>
            <div slot="minlength" class="alert alert-danger mt-1">Este campo debe poseer al menos {{caracterMinimo}} caracteres</div>
            <div v-if="formData.apellido && (formData.apellido.length == 15)" class="alert alert-danger mt-1">Este campo debe poseer como máximos {{caracterMaximo}} caracteres</div>
            <div slot="no-espacios" class="alert alert-danger mt-1">Este campo no permite espacios intermedios</div>
          </field-messages>
        </validate>
        <br>
        
        <validate tag="div">
          <label for="nota">Ingrese la nota:</label>
          <input 
          type="number" 
          id="nota" 
          v-model.number="formData.nota" 
          required 
          :min="notaMinima"
          :max="notaMaxima"
          name="nota" 
          autocomplete="off" 
          class="form-control" />
    
          <field-messages name="nota" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio</div>
            <div slot="min" class="alert alert-danger mt-1">La nota minima es {{notaMinima}} </div>
            <div slot="max" class="alert alert-danger mt-1">La nota maxima es {{notaMaxima}}</div>
          </field-messages>
        </validate>

        <br>
        
        <button class="btn btn-success my-3" :disabled="formstate.$invalid" type="submit">Enviar</button>
      </vue-form>
      <br>
      <hr>
      <hr>

      <h2>Historial de notas:</h2>
      <hr>
      <div v-if="notas.length" class="table-responsive">
        <table class="table">
          <tr>
            <th>Alumno</th>
            <th>Nota</th>
          </tr>
          <tr v-for="(notaAlumno,index) in notas" :key="index">
            <td>{{ notaAlumno.nombre + " " + notaAlumno.apellido }}</td>
            <td :style="{color: dameColor(notaAlumno.nota).color}">
            {{dameColor(notaAlumno.nota).nota}}</td>
          </tr>
          <tr :style="{color: PromedioTotal().color}">
            
            <th>Promedio total:</th>
            <th>{{PromedioTotal().total}}</th>
            <td></td> 
          </tr>
        </table>
      </div>
      <h4 v-else class="alert alert-danger">No hay notas ingresadas</h4>

    </div>
  </section>

</template>

<script>

  export default  {
    name: 'src-componentes-ingreso',
    props: [],
    mounted () {

    },
    data () {
      return {
        formstate : {},
        formData : this.getInitialData(),
        notas : [],
        notaMinima:0,
        notaMaxima:10,
        caracterMinimo:3,
        caracterMaximo:15
      }
    },
    methods: {
      getInitialData() {
        return {
          nombre : null,
          apellido: null,
          nota: null
        }
      },
      enviar() {
        let nota = {...this.formData}
        this.notas.push(nota)

        this.formData = this.getInitialData()
        this.formstate._reset()
      },
      PromedioTotal() {
        let total = 0
        let cantAlumnos=0
        this.notas.forEach(notaAlumno => {
          total += notaAlumno.nota 
          cantAlumnos = cantAlumnos + 1
        })
        total = total / cantAlumnos


        let color = ''
        if(total >= 0 && total <= 3) color = 'red'
        else if(total >= 4 && total <= 6) color = 'yellow'
        else if(total >= 7 && total <= 10) color = 'green'
        return {
          total,
          color
        }
      },
      dameColor(nota){
          let color = ''
        if(nota >= 0 && nota <= 3) color = 'red'
        else if(nota >= 4 && nota <= 6) color = 'yellow'
        else if(nota >= 7 && nota <= 10) color = 'green'
        return {
          nota,
          color
        }
      }
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

  pre {
    color: white;
  }
</style>
