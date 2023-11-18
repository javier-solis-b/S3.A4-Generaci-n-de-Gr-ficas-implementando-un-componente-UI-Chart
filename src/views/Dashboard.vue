<template>
  <div id="app">
  <div class="container">
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css">
  </div> 
 
  <!-- <div class="container">  -->
    <div class="row">
      <!-- Mensaje de bienvenida en el lateral izquierdo -->
      <div class="col-md-3">
        <div class="layout-sidebar">
          <img src="public\demo\images\Fondo\Logohcs.png" style="width: 70%; border-radius: 20px; margin: 0 auto; display: block; box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);">
         <h2 class="mensaje"> ¡Bienvenido al Restaurante! </h2>
         <h5 class="mensaje2"> Esperamos que disfrutes de nuestra deliciosa comida.</h5>
         <h6 class="mensaje3"> Selecciona los platillos, después da clic en el botón "Enviar pedido"</h6>
        <h6 class="mensaje4"> ¡Buen provecho!</h6>
        </div>
      </div>
    </div>

 <div class="container">
        <div v-if="!pedidoIniciado"> 
   <!-- Formulario para el nombre del cliente  -->
  <div class="row">
    <div class="col-md-6 offset-md-3">
      <div class="form-group">
        <label for="customerName">Nombre del Cliente:</label>
        <input type="text" class="form-control" v-model="customerName" id="customerName" placeholder="Ingrese su nombre">
      </div>
      <!-- <button class="btn btn-primary" @click="startOrder">Iniciar Pedido</button> -->
    </div>
  </div>
  </div> 
      </div> 
    
    <!-- MENU DEL RESTAURANTE -->
  <div class="container"> 
  <div v-if="!pedidoIniciado">
   <h1 class="my-4">Menú del Restaurante HCS</h1>
   <div class="row">
     <div v-for="(dish, index) in dishes" :key="index" class="col-md-4 mb-4">
       <div class="card">
         <div class="card-body">
          
           <h5 class="card-title">{{ dish.name }}</h5>
           <p class="card-text">Precio:$ {{ dish.price }}</p>
           <div class="input-group mb-3">
             <input type="number" class="form-control" v-model="dish.quantity" placeholder="Cantidad">
             <div class="input-group-append">
              <button class="btn btn-primary" @click="addToOrder(dish)">Agregar al pedido</button> -
             </div>
           </div>
         </div>
       </div>
     </div>
   </div>
   </div>

   <div class="my-4">
     <h2>Resumen del pedido</h2>
     <p>Cliente: {{ customerName }}</p>
     <p>Fecha y Hora del Pedido: {{ getCurrentDateTime() }}</p> 
     <div v-for="(item, index) in order" :key="index" class="mb-2">
       <p>{{ item.name }}: {{ item.quantity }} - Precio unitario: ${{ item.price }} </p>
       <button class="btn btn-danger btn-sm ml-2" @click="removeFromOrder(item)">Eliminar</button>
     </div>
     <p>Total: ${{ total }}</p> <!-- Muestra el total -->
     <button class="btn btn-primary" @click="startOrder">Enviar Pedido</button>
    <!--  <button @click="iniciarPago">Pagar Ahora</button> -->
     <!-- <button class="btn btn-secondary" @click="goToMenu">Volver al Menú</button>  -->
     <!-- <button class="btn btn-success" @click="submitOrder">Enviar pedido</button> -->
   </div>
  </div>
</div>


</template>
   <!--  </div> -->
<!--  </template>  -->
 
<script>
 export default {
  data() {
   return {
     customerName: '',
     dishes: [
       // Aquí puedes agregar los platos disponibles
       { name: 'Enchiladas',  price: 70, quantity: 1 },
       { name: 'Chilaquiles', price: 60, quantity: 1 },
       { name: 'Enfrijoladas',  price: 70, quantity: 1 },
       { name: 'Pechuga empanizada',  price: 90, quantity: 1 },
       { name: 'Flautas',  price: 70, quantity: 1 },
       { name: 'Milanesa',  price: 90, quantity: 1 },
       { name: 'Pozole',  price: 90, quantity: 1 },
       { name: 'Huevos ranchero',  price: 60, quantity: 1 },
       // Agrega más platos según sea necesario
     ],
     order: [],
     total: 0,
     pedidoIniciado: false,
   };
  },
  methods: {
  startOrder() {
    if (this.customerName.trim() !== '') {
      this.pedidoIniciado = true;
      console.log(`¡Hola, ${this.customerName}! Pedido iniciado.`);
    } else {
      alert('Por favor, ingrese su nombre antes de iniciar el pedido.');
    }
  }, 
   addToOrder(dish) {
     // Aquí puedes agregar la lógica para agregar un plato al pedido
     const existingDish = this.order.find(item => item.name === dish.name);
    
    if (existingDish) {
      // Si el platillo ya está en el pedido, incrementa la cantidad.
      existingDish.quantity++;
    } else {
      // Si no está en el pedido, agrégalo con cantidad 1.
      this.order.push({ ...dish, quantity: 1 });
    }
    this.calculateTotal();
  },
  removeFromOrder(dish) {
    const index = this.order.findIndex(item => item.name === dish.name);

    if (index !== -1) {
      const currentQuantity = this.order[index].quantity;

      // Si hay más de un platillo, simplemente decrementa la cantidad.
      if (currentQuantity > 1) {
        this.order[index].quantity--;
      } else {
        // Si hay solo un platillo, elimina el elemento del pedido.
        this.order.splice(index, 1);
      }

      this.calculateTotal();
    }
  },
  getCurrentDateTime() {
      const now = new Date();
      const formattedDate = `${now.getDate()}/${now.getMonth() + 1}/${now.getFullYear()}`;
      const formattedTime = `${now.getHours()}:${now.getMinutes()}:${now.getSeconds()}`;
      return `${formattedDate} ${formattedTime}`;
    },
  
  calculateTotal() {
    this.total = this.order.reduce((accumulator, item) => {
      return accumulator + item.price * item.quantity;
    }, 0);
  },
   submitOrder() {
     // Aquí puedes agregar la lógica para enviar el pedido
     console.log('Pedido enviado:', this.order);
   },
  },
};

  </script> 

<style>
#app {
background-color: #8FBC8F; /* Color de fondo para el dashboard */
  padding: 20px; /* Ajusta el espaciado según tus preferencias */
/*   width: 600px; */ /* Ancho exacto del dashboard */
 /*  margin: 0 auto; */ /* Centra el dashboard en la página */
}

/* Otros estilos aquí... */

</style>
 
