<template>
  <div class="container">
    <div class="card">
      <div class="card-header">Agregar un Nuevo Empleado</div>
      <div class="card-body">
        <form v-on:submit.prevent="agregarRegistro"> <!--Llamar a la funcion -->
          <div class="form-group">
            <label for="nombre">Nombre:</label>
            <input
              type="text"
              class="form-control"
              required name="nombre"
              id="nombre"
              aria-describedby="helpId"
              placeholder="Nombre"
              v-model="empleado.nombre"
              
            />
            <small id="helpId" class="form-text text-muted"
              >Escribe el nombre del Empleado</small>
          </div>

          <div class="form-group">
            <label for="">Correo:</label>
            <input
              type="email"
              class="form-control"
              required name="correo"
              id="correo"
              aria-describedby="helpId"
              placeholder="Correo"
              v-model="empleado.correo"
            />
            <small id="helpId" class="form-text text-muted"
              >Escribe el correo del empleado</small
            >
          </div>

          <div class="btn-group" role="group" aria-label="">
            <button type="submit" class="btn btn-success">Agregar</button>
            <router-link :to="{name:'Listar'}" class="btn btn-warning"> Cancelar</router-link>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
    data(){
        return{
            empleado:{} //ESTE EMPLEADO TENDRA DATOS
        }
    },
    methods:{
        agregarRegistro(){
            console.log(this.empleado)
            var datosEnviar ={
                nombre:this.empleado.nombre,
                correo:this.empleado.correo
                }

                fetch('http://localhost/empleados/?insertar=1',{
                    method:"POST",
                    body:JSON.stringify(datosEnviar)

                })
                .then(respuesta=>respuesta.json())
                .then((datosRespuesta=>{
                    console.log(datosRespuesta)
                    window.location.href='listar'
                }))
                .catch(e)    
        }
    }
};
</script>

<style>
</style>