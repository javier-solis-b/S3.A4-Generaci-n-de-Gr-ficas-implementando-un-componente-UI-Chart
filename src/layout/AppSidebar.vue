<script setup>
import AppMenu from './AppMenu.vue';
</script>

<template><!-- 
     <div class="row"> -->
      <!-- Mensaje de bienvenida en el lateral izquierdo -->
      <!-- <div class="col-md-3">
        <div class="layout-sidebar">
         <h2 class="mensaje"> ¡Bienvenido al Restaurante HCS! </h2>
         <h5 class="mensaje2"> Disfruta de nuestra deliciosa comida.</h5>
         <h6 class="mensaje3"> Selecciona los platillos, después da clic en el botón "Enviar pedido"</h6>
        </div>
      </div>
     </div> -->
    <app-menu></app-menu>
</template>


<!-- <style lang="scss" scoped></style> -->
<style>
.layout-sidebar {
  background-color: #f8f9fa; /* Color de fondo */
  padding: 20px; /* Espaciado interno */
  border-radius: 8px; /* Bordes redondeados */
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1); /* Sombra ligera */
}

.mensaje {
  color: #0059ff; /* Color del texto principal */
  margin-bottom: 20px; /* Espaciado inferior */
}

.mensaje2 {
  color: #28a745; /* Color del texto secundario */
  margin-bottom: 20px; /* Espaciado inferior */
}

.mensaje3 {
  color: #6c757d; /* Color del texto adicional */
}
</style>