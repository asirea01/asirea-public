<template>
  <header class="container-fluid" :class="{ 'header-transparent': isScrolled }">
    <!-- Móvil -->
    <div class="mainHamburger">
      <div class="cnavmovil">
        <a class="ctitle" href="/">
          <img src="/images/logo.webp" alt="logo" />
          <span class="chidemovil">ASIREA</span>
        </a>
        <a id="hamburgerMenuButton" class="ctitle" @click="$emit('toggleMenu')">
          <i class="bi bi-list clist"></i>
        </a>
      </div>
    </div>

    <!-- Escritorio -->
    <div class="row chead mainMenu mx-0">
      <div class="col-md-2 cmidle">
        <a class="ctitle" href="/">
          <img src="/images/logo.webp" />
          <span class="cmidle">ASIREA</span>
        </a>
      </div>

      <div class="col-md-10">
        <ul class="cnav">
          <li
            v-for="item in menu"
            :key="item.href"
            :active="$route.path === item.href ? '' : null"
          >
            <router-link
              :to="item.href"
              data-bs-toggle="tooltip"
              data-bs-placement="bottom"
              :title="item.text"
            >
              <i :class="['bi', item.icon, 'cicon']"></i>
            </router-link>
          </li>
        </ul>
      </div>
    </div>
  </header>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import { Tooltip } from 'bootstrap';

const isScrolled = ref(false);
let tooltipInstances = [];

function handleScroll() {
  isScrolled.value = window.scrollY > 50;
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
  const tooltipEls = document.querySelectorAll('[data-bs-toggle="tooltip"]');
  tooltipInstances = [...tooltipEls].map(el => new Tooltip(el));
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
  tooltipInstances.forEach(t => t.dispose());
});

const menu = [
  { text: "Inicio",        icon: "bi-house",         href: "/" },
  { text: "Servicios",     icon: "bi-card-list",      href: "/services" },
  { text: "Trayectoria",   icon: "bi-file-earmark",   href: "/trajectory" },
  { text: "¿Quienes somos?", icon: "bi-people",       href: "/who_are_we" },
  { text: "Donar",         icon: "bi-coin",           href: "/donate" },
  { text: "Contacto",      icon: "bi-telephone",      href: "/contact" },
];
</script>

<style scoped>
/* ============================================================
   HEADER BASE
   ============================================================ */
header {
  background-color: #014a36;
  color: #fff !important;
  position: fixed;
  height: 90px;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 1030;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 20px;
}

/* Neutraliza el padding acumulado de Bootstrap .container-fluid */
header.container-fluid {
  width: 100%;
  max-width: 100%;
  overflow-x: hidden;
  padding-left: 0 !important;
  padding-right: 0 !important;
  transition: background-color 0.3s ease;
}

.header-transparent {
  background-color: rgba(90, 98, 93, 0.737) !important;
  backdrop-filter: blur(8px);
  transition: background-color 0.3s ease;
}

/* ============================================================
   LOGO / TÍTULO
   ============================================================ */
.chead {
  width: 100%;
  height: 70px;
}

.ctitle {
  padding-top: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 50px;
  color: #fff;
  text-decoration: none;
}

.ctitle:hover,
.ctitle:active,
.ctitle:visited {
  color: #fff;
  text-decoration: none;
}

.ctitle img {
  height: 40px;
  width: auto;
}

.ctitle span {
  font-size: 35px;
  padding-left: 20px;
  padding-bottom: 0;
}

/* ============================================================
   NAV ESCRITORIO
   ============================================================ */
.cnav {
  width: 100%;
  list-style: none;
  justify-content: center;
  padding: 10px 0;
  display: flex;
  margin: 0;
}

.cnav li {
  text-align: center;
  margin: 0 15px;
  width: 16%;
  border-bottom: 1px solid transparent;
  border-image: linear-gradient(to right, rgba(0,0,0,0), rgba(0,0,0,0)) 1;
}

.cnav li:hover,
.cnav li[active] {
  animation: border_animation 0.25s forwards;
}

.cnav a {
  color: #fff;
  text-decoration: none;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px 0;
}

.cnav a:hover,
.cnav a:active,
.cnav a:visited {
  color: #fff;
  text-decoration: none;
}

.cicon {
  font-size: 25px;
  margin-right: 20px;
}

/* ============================================================
   LAYOUT ESCRITORIO / MÓVIL
   ============================================================ */
.cmidle {
  display: inline;
}

.mainHamburger {
  display: none;
  max-width: 100dvw;
}

.mainMenu {
  display: flex;
}

/* ============================================================
   ANIMACIÓN BORDE NAV
   ============================================================ */
@keyframes border_animation {
  0% {
    border-bottom: 2px solid transparent;
    border-image: linear-gradient(to right,
      rgba(255,255,255,0), rgba(255,255,255,0),
      rgba(255,255,255,0), rgba(255,255,255,0),
      rgba(255,255,255,0)) 1;
  }
  25% {
    border-bottom: 1px solid transparent;
    border-image: linear-gradient(to right,
      rgba(255,255,255,0), rgba(255,255,255,0),
      rgba(255,255,255,1), rgba(255,255,255,0),
      rgba(255,255,255,0)) 1;
  }
  50% {
    border-bottom: 1px solid transparent;
    border-image: linear-gradient(to right,
      rgba(255,255,255,0), rgba(255,255,255,1),
      rgba(255,255,255,1), rgba(255,255,255,1),
      rgba(255,255,255,0)) 1;
  }
  75% {
    border-bottom: 1px solid transparent;
    border-image: linear-gradient(to right,
      rgba(255,255,255,0.5), rgba(255,255,255,1),
      rgba(255,255,255,1),   rgba(255,255,255,1),
      rgba(255,255,255,0.5)) 1;
  }
  100% {
    border-bottom: 1px solid transparent;
    border-image: linear-gradient(to right,
      rgba(255,255,255,1), rgba(255,255,255,1),
      rgba(255,255,255,1), rgba(255,255,255,1),
      rgba(255,255,255,1)) 1;
  }
}

/* ============================================================
   MEDIA QUERY — MÓVIL (≤ 1600px oculta texto central)
   ============================================================ */
@media screen and (max-width: 1600px) {
  .cmidle {
    display: none;
  }

  .mainHamburger {
    display: none;
  }

  .mainMenu {
    display: block;
  }
}

/* ============================================================
   MEDIA QUERY — MÓVIL (≤ 775px activa hamburguesa)
   ============================================================ */
@media screen and (max-width: 775px) {
  .cnav {
    display: none;
  }

  .chidemovil {
    display: none;
  }

  .ctitle {
    width: auto;
    justify-content: center;
    align-items: center;
  }

  /* Ícono hamburguesa */
  .clist {
    display: block;
    font-size: 50px;
    margin-right: 10px;
  }

  /* Barra superior móvil */
  .cnavmovil {
    display: flex;
    width: 100%;    
    justify-content: space-between;
    padding: 0 10px;
  }

  .mainHamburger {
    display: block;
    width: 100%;
  }

  .mainMenu {
    display: none;
  }
}
</style>
