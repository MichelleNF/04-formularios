<template>
      <div class="row">
        <div class="col-12 col-md-4">
          <h3 class="text-center">Progreso {{ porcentaje }}%</h3>
          
          <div class="progress">
            <div class="progress-bar progress-bar-striped progress-bar-animated bg-succss" role="progressbar" :aria-valuenow="porcentaje" aria-valuemin="0" aria-valuemax="100" :style="`width: ${porcentaje}%`" >
            </div>
          </div>
        </div>

          <form @submit.prevent="registrarProyecto">
            <div class="mb-3">
              <label class="form-label">Proyecto </label>
              <input v-model.trim="proyecto" type="text" class="form-control" required/>
            </div>
    
            <div class="mb-3">
              <label class="form-label">Actividad</label>
              <select v-model.trim="tipo" class="form-select" required>
                <option disabled selected value="">Seleccione tipo de actividad ...</option>
                <option>Aplicaciones Web con Vue.js</option>
                <option>Backend Service con Node.js</option>
                <option>App Movil con Rest Native</option>
              </select>
            </div>
    
            <div class="mb-3">
                <label for="exampleInputPassword1" class="form-check-label">Urgente</label>
                <input v-model.trim="urgente" type="checkbox" class="form-check-input">
              </div>
            
            <button type="submit" class="btn btn-primary">Guardar</button>
          </form>
        
        <div class="col-12 col-md-8">
            <total-proyectos 
              :numeroProyectos="numeroProyectos"
              :proyectos="proyectos"
              :cambiarEstado="cambiarEstado"
            />       
      </div>
    </div>
</template>

<script>
  import TotalProyectos from "./TotalProyectos.vue";

  export default {
      data: () => ({
          proyecto: "",
          tipo: "",
          urgente: false,
          proyectos: [],
      }),
      methods: {
          registrarProyecto () {
              const proyecto = {
                  proyecto: this.proyecto,
                  tipo: this.tipo,
                  urgente: this.urgente,
              };
              this.proyectos.push(proyecto);
              this.proyecto = "";
              this.tipo = "";
              this.urgente = false;
          },
          cambiarEstado(id) {
            //this.urgente = !this.urgente; //con ! se niega
            this.proyectos[id].urgente = !this.proyectos[id].urgente;
          }
      },
      computed: {
        numeroProyectos(){
          return this.proyectos.length;
        },
        porcentaje (){
          let completados = 0;
          this.proyectos.map(proyecto => {
            if (proyecto.completado)
              completados++;
          });
          return (completados * 100) / this.numeroProyectos || 0;
        }
      },
      components: { TotalProyectos }
  };
</script>