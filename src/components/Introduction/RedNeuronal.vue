<template>
    <router-link to=""></router-link>
<body class="page page-home preload">

<header class="header-main dark">
  <nav>
    <a href="/lobby-one" class="logo" rel="home"><svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" width="24" height="24" viewBox="0 0 24 24"><path d="M7.335 1.023l2.462.434a1 1 0 0 1 .811 1.159L8.004 17.388a2 2 0 0 1-2.317 1.622l-3.94-.694a1 1 0 0 1-.81-1.159L3.28 3.862a3.5 3.5 0 0 1 4.054-2.839zm7.039 3.272l7.878 1.39a1 1 0 0 1 .812 1.158l-1.997 11.325a5.5 5.5 0 0 1-6.372 4.461l-4.431-.78a1 1 0 0 1-.812-1.16l2.605-14.771a2 2 0 0 1 2.317-1.623z" fill="currentColor"/></svg><span>Polinder</span></a>
      <div class="nav-toggle"></div>
      <ul class="inline">
        <li><a href="/lobby-two" class="active">Inicio</a></li>
        <li><a href="/my-account">Mi cuenta</a></li>
        <li><a href="/red-neuronal">Descarga</a></li>
        <li><a href="/help-page">Ayuda</a></li>
        <li><a href="/login-page">Cerrar sesión</a></li>
    </ul>
    <ul class="inline right">
      <li>{{ usuarios.nombre }}</li>
      <li><div class="avatar"> 
        <!-- Avatar image -->
        <img class="avatar__image"  :src="require(`../../media/${usuarios.imagen}`)"/>
        </div>
      </li>
    </ul>
  </nav>
</header>

<main>
  <section class="bg-image-hero center-tablet dark overlay-hero">
    <div class="full-screen -margin-bottom middle padding padding-top-tablet">
      <div class="row max-width-l">
        <div class="col-one-half middle">
          <div>
            <h1 class="hero">Inteligencia Artificial</h1>
            <p class="lead">Aqui puedes descargar nuestra aplicacions de reconocimienta facial hecha con inteligencia artificial.</p>
            <a :href="archivoURL" target="_blank">
               <button class="download-button">Descargar archivo</button>
            </a>
          </div>
        </div>
        <div class="col-one-half middle">
          <img src="../../media/content/inteligencia.jpg" alt="Hero Illustration">
        </div>
      </div>
    </div>
  </section>

</main>

<footer class="footer-main bg-gradient-primary dark overlay-shape-06">
  <div class="padding">

    
    <div class="row center-desktop max-width-l">
      <div class="col-two-fifths">
        <h6>Polinder ®</h6>
        <p>Somos una empresa completamente remota que trabaja en veinte países con más de 20 000 clientes.</p>
      </div>
      <div class="col-one-fifth">
        <h6>Informacion</h6>
        <ul class="blank">
          <li><a href="#">Empezando</a></li>
          <li><a href="#">Recursos</a></li>
          <li><a href="#">Diseno</a></li>
          <li><a href="#">Tutoriales</a></li>
          <li><a href="#">Precios</a></li>
        </ul>
      </div>
      <div class="col-one-fifth">
        <h6>Soporte</h6>
        <ul class="blank">
          <li><a href="#">Documentación</a></li>
          <li><a href="#">Requisitos</a></li>
          <li><a href="#">Licencia</a></li>
          <li><a href="#">Actualizaciones</a></li>
          <li><a href="#">Contacto</a></li>
        </ul>
      </div>
      <div class="col-one-fifth">
        <h6>Contactos</h6>
        <ul class="blank">
          <li><a href="#">Twitter</a></li>
          <li><a href="#">Facebook</a></li>
          <li><a href="#">Instagram</a></li>
          <li><a href="#">Medium</a></li>
        </ul>
      </div>
    </div>
  </div>
  <p class="copyright"><span>HTML Template by </span><a href="https://uiuxassets.com/" target="_blank">UI/UX Assets</a><span> - © 2018, all rights reserved.</span></p>
</footer>

</body>
</template>

<script>
import axios from 'axios';

export default {

  name: 'red-neuronal',
  data() {
    return {
      archivoURL: 'https://drive.google.com/file/d/1RFTG-au4VlPyD2HXyWwJaDM4lxsCz808/view?usp=sharing',
        usuarios: {
        email: "",
        password: "",
        nombre: "",
        apellido: "",
        boleta: "",
        telefono: "",
        escuela: "",
        planRelacion: "",
        descripcion: "",
        imagen: ""
      },
    };
  },
  methods: {

  },

    created() {


    // Realiza la solicitud POST para obtener los datos del usuario
    var bodyFormData = new FormData();
    bodyFormData.append('id', window.localStorage.getItem("IdUsuario")); 
    

    axios.post('http://localhost/Backend.php', bodyFormData)
    .then(response => {
      // Asigna los datos del usuario a las variables del componente
      this.usuarios.email = response.data.email;
      this.usuarios.password = response.data.password;
      this.usuarios.nombre = response.data.nombre;
      this.usuarios.apellido = response.data.apellidos;
      this.usuarios.boleta = response.data.boleta;
      this.usuarios.telefono = response.data.telefono;
      this.usuarios.escuela = response.data.escuela;
      this.usuarios.planRelacion = response.data.plan_relacion;
      this.usuarios.descripcion = response.data.descripcion;
      this.usuarios.imagen = response.data.imagen;

      console.log(response.data.imagen);
      bodyFormData.append('escuela', this.usuarios.escuela);

    })
    .catch(error => {
      console.error(error);
    });
  },

}
</script>

<style scoped>
 .download-button {
  background-color: green;
  color: white;
  border: none;
  border-radius: 20px;
  padding: 10px 20px;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  cursor: pointer;
}
</style>
