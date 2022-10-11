<script>
    export default {
        data: () => ({

        }),
        methods: {
            registrarProyecto (){
                console.log("Proyecto resistrado...")
            },
        },
    };
</script>

<template>
    <form @submit.prevent="registrarProyecto">
        <div class="mb-3">
          <label class="form-label">Proyecto</label>
          <input type="text" class="form-control" required/>
        </div>

        <div class="mb-3">
          <label class="form-label">Actividad</label>
          <select class="form-select" required>
            <option disabled selected value="">Seleccione tipo de actividad ...</option>
            <option>Aplicaciones Web con Vue.js</option>
            <option>Backend Service con Node.js</option>
            <option>App Movil con Rest Native</option>
          </select>
        </div>

        <div class="mb-3">
            <label for="exampleInputPassword1" class="form-check-label">Urgente</label>
            <input type="checkbox" class="form-check-input">
          </div>
        
        <button type="submit" class="btn btn-primary">Guardar</button>
      </form>
</template>