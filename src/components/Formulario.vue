<template>

  <section class="formulario">
    <div class="jumbotron">
    <h1>Formulario con Vue-Form</h1>
    <hr>
    <br>
      <vue-form :state="formState" @submit.prevent="enviar()">

        <validate tag="div">
          <label for="nombre"> Nombre</label>
          <input 
          type="text"
          id="nombre"
          name="nombre"
          class="form-control"
          v-model.trim="formData.nombre"
          required
          autocomplete="off"
          :minlength="nameMinLength"
          :maxlength="nameMaxLength"
          >
          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio</div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Ingrese al menos {{nameMinLength}} caracteres
            </div>
            <div v-if="formData.nombre.length == nameMaxLength" class="alert alert-warning mt-1">
              Ingrese menos de {{nameMaxLength}} caracteres
            </div>
          </field-messages>
        </validate>

        <br>
        
        <validate tag="div">
          <label for="edad"> Edad</label>
          <input 
          type="number"
          id="edad"
          name="edad"
          class="form-control"
          autocomplete="off"
          v-model.number="formData.edad"
          :min="edadMin"
          :max="edadMax"
          >
        </validate> 
        <field-messages name="edad" show="$dirty">
          <div slot="min" class="alert alert-danger mt-1">Edad minima: {{edadMin}}</div>
          <div slot="max" class="alert alert-danger mt-1">Edad maxima: {{edadMax}}</div>
          <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio</div>
        </field-messages>
        <br>
        
        <validate tag="div">
          <label for="email">Email </label>
          <input 
          type="email"
          id="email"
          name="email"
          class="form-control"
          autocomplete="off"
          required
          v-model.trim="formData.email"
          >
        </validate>
        <field-messages name="email" show="$dirty">
          <div slot="required" class="alert alert-danger mt-1">Este campo es obligatorio</div>
          <div slot="email" class="alert alert-danger mt-1">Email no valido</div>
        </field-messages>
        <br>
        <br>        
        <button class="btn btn-info my3" :disabled="formState.$invalid" type="submit">Enviar</button>

      </vue-form>
      <br>
      <hr>
      <table class="table table-striped table-bordered table-sm">
        <thead class="thead-dark">
        <tr>
          <th>Nombre</th>
          <th>Edad</th>
          <th>Mail</th>
        </tr>
         </thead>
        <tr>
          <td>{{formData.nombre}}</td>
          <td>{{formData.edad}}</td>
          <td>{{formData.email}}</td>
        </tr>
      </table>
    </div>
  </section>

</template>

<script>

  export default  {
    name: 'formulario',
    props: [],
    mounted () {

    },
    data () {
      return {
        formData:this.getInitialData(),
        formState:{},
        edadMin : 18,
        edadMax : 120,
        nameMinLength : 5,
        nameMaxLength: 15,
      }
    },
    methods: {
      getInitialData(){
        return {
          nombre:"",
          edad:"",
          email:"",
        }
      },
      enviar(){
        console.log({...this.formData});
        this.formData=this.getInitialData()
        this.formState._reset()
      }
    },
    computed: {

    }
}


</script>

<style scoped>
.jumbotron{
    background-color: rgb(250, 250, 250);
    
}

</style>
