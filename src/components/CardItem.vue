<template>
  <div class="ccard" @mouseover="hover = true" @mouseleave="hover = false">
    <div class="ccardhead">{{ data.titulo }}</div>
    <div class="ccardbody">
      <img :src="data.imagenPortadaUrl || 'images/noticia-default.png'" :class="['ccardimg', {'default-img': !data.imagenUrl}]" />
      <div class="ccardtext" :class="hover ? 'animationin' : 'animationout'">
        <p>{{ shortText }}</p>
        <button class="btn btn-primary active ccarda" @click="$emit('show-modal', data)">
          Mostrar más
        </button>
      </div>
    </div>
    <div class="ccardfoot">
      <a v-if="isButton"
        class="btn btn-primary active ccarda"
        :href="data.documentos[0]?.url"
        :target="targetBlank ? '_blank' : '_self'"
      >
        {{ buttonText }}
      </a>
    </div>
  </div>
</template>

<script setup>
import { computed, ref } from 'vue'

const props = defineProps({
  data: Object,
  isButton: Boolean,
  buttonText: String,
  targetBlank: Boolean
})

const hover = ref(false)
const shortText = computed(() =>
  props.data.descripcion.length > 75 ? props.data.descripcion.slice(0, 75) + '...' : props.data.descripcion
)
</script>

<style scoped>
/* ============================================================
   CARD CONTENEDOR
   ============================================================ */
.ccard {
    flex-shrink: 0;
    flex-grow: 0;
    border: #014a36 5px solid;
    background-color: #fff;
    border-radius: 5px;
    height: 425px;
    width: 400px;
}

/* ============================================================
   CARD HEAD
   ============================================================ */
.ccardhead {
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    padding-left: 20px;
    padding-right: 20px;
    width: 390px;
    height: 115px;
    color: #fff;
    background-color: #014a36;
    font-size: 25px;
    overflow: hidden;
}

/* ============================================================
   CARD BODY + IMAGEN
   ============================================================ */
.ccardbody {
    font-size: 22px;
    width: 390px;
    height: 225px;
    background-color: #777;
    text-align: center;
    overflow: hidden;
    transition: transform 0.4s ease-out;
}

.ccardimg {
    width: auto;
    height: 225px;
}

.default-img {
    background-color: #2b1f11;
}

/* ============================================================
   CARD TEXT (overlay deslizante)
   ============================================================ */
.ccardtext {
    width: 390px;
    height: 225px;
    padding: 15px;
    background-color: #f0f0f0cf;
    color: black;
    overflow-y: auto;
    overflow-x: hidden;
    position: relative;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
    z-index: 10;
    opacity: 0.90;
}

.ccardtext.animationin {
    animation-name: ccardmovein;
    animation-duration: 1.5s;
    animation-timing-function: ease-in-out;
    animation-fill-mode: forwards;
}

.ccardtext.animationout {
    animation-name: ccardmoveout;
    animation-duration: 1.5s;
    animation-timing-function: ease-in-out;
    animation-fill-mode: forwards;
}

@keyframes ccardmovein {
    0%   { transform: translateY(0px); }
    100% { transform: translateY(-225px); }
}

@keyframes ccardmoveout {
    0%   { transform: translateY(-225px); }
    100% { transform: translateY(0); }
}

/* ============================================================
   CARD FOOT
   ============================================================ */
.ccardfoot {
    padding-top: 10px;
    width: 100%;
    height: 75px;
    color: #fff;
    background-color: #014a36;
    text-align: center;
}

/* ============================================================
   BOTÓN CTA DE CARD
   ============================================================ */
.ccarda {
    text-decoration: none;
    display: inline-block;
    cursor: pointer;
    color: #000 !important;
    background-color: #ffb209 !important;
    width: 200px;
    height: 48px;
    font-size: 1.2rem;
    border-radius: 10px;
    padding: 10px 25px;
    font-weight: 800;
    margin-bottom: 2%;
    border: 0 !important;
}

.ccarda:hover {
    background-color: #fae7c2 !important;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}
</style>