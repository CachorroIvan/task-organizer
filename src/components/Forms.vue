<script>
import ProgressBar from './ProgressBar.vue'
import TotalProyectos from './TotalProyectos.vue'
export default{
  components: {
    ProgressBar, TotalProyectos
  },
  data: () => ({
    proyecto: "",
    tipo: "",
    urgente: false,
    proyectos: [],

  }),
  methods: {
    registrarProyecto(){
      
      
      const proyecto = {
        proyecto: this.proyecto,
        tipo: this.tipo,
        urgente: this.urgente,
        completado: false,
      };

      this.proyectos.push(proyecto)

      this.proyecto = "";
      this.tipo = "";
      this.urgente = false;
      },

      cambiarEstado(proyecto, campo) {
        //this.proyectos[id].urgente = !this.proyectos[id].urgente;
        proyecto[campo] = !proyecto[campo];
    }
  },
  computed: {
    numeroProyectos() {
      return this.proyectos.length;
    },
    porcentaje(){
      let completados = 0;

      this.proyectos.map(proyecto => {
        if(proyecto.completado) completados++
      });
      return completados * 100 / this.numeroProyectos || 0;
    }
  }
}
</script>


<template>
    <div class="row">
      <progress-bar :porcentaje="porcentaje" />
      <div class="col-12 col-md-4">
        <form @submit.prevent="registrarProyecto">
          <div class="mb-3">
              <label class="form-label">Proyecto </label>
              <input v-model="proyecto" type="text" class="form-control" required>
          </div>
          <div class="mb-3">
              <label class="form-label">Actividad </label>
              <select v-model="tipo" class="form-select" required>
                <option disabled selected value="">Seleccione un tipo</option>
                <option >Aplicacion web con vue.js</option>
                <option >Backend Service con Node.js</option>
                <option >App movile con React Native</option>
              </select>
          </div>
          <div class="mb-3">
              <label for="exampleInputPassword1" class="form--check-label">Urgente</label>
              <input type="checkbox" v-model="urgente" class="form-check-input" >
          </div>
          
          <button type="submit" class="btn btn-primary">Guardar</button>
        </form>
      </div>
        <div class="col-12 col-md-8">
          <total-proyectos :numeroProyectos="numeroProyectos" 
          :proyectos="proyectos"
          :cambiar-estado="cambiarEstado"/>
        </div>
    </div>
</template>