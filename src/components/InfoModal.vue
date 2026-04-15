<template>
  <Teleport to="body">

    <Transition name="modal">
      <div class="modal-backdrop-custom" @click.self="close" v-if="visible">
        <div class="modal-box">
          <div class="modal-header ccardModalHead">
            <h4 class="modal-title">{{ item.titulo }}</h4>
          </div>
          <div class="modal-body ccardModalBody">
            <div class="modal-image-wrapper">
              <img :src="item.imagenPortadaUrl" class="modal-image" />
            </div>
            <div class="modal-right-col">
              <div v-if="fechaFormateada" class="modal-date-chip">
                <svg xmlns="http://www.w3.org/2000/svg" width="13" height="13" fill="currentColor" viewBox="0 0 24 24">
                  <path
                    d="M19 4h-1V2h-2v2H8V2H6v2H5C3.9 4 3 4.9 3 6v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2m0 16H5V10h14zm0-12H5V6h14z" />
                </svg>
                {{ fechaFormateada }}
              </div>
              <div class="modal-description" v-html="item.descripcion"></div>
            </div>
          </div>
          <div class="modal-footer ccardModalFoot">
            <button class="btn btn-primary ccarda" @click="close">Cerrar</button>
          </div>
        </div>
      </div>
    </Transition>
  </Teleport>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue'

const props = defineProps({ item: Object })

const fechaFormateada = computed(() => {
  if (!props.item?.fechaCreacion) return null

  return new Date(props.item.fechaCreacion).toLocaleDateString('es-ES', {
    day: '2-digit',
    month: 'long',
    year: 'numeric'
  })
})
const emit = defineEmits(['close'])
const visible = ref(false)

onMounted(() => {
  visible.value = true
  document.body.style.overflow = 'hidden'
})

function close() {
  visible.value = false
  document.body.style.overflow = ''
  setTimeout(() => emit('close'), 300)
}
</script>

<style scoped>
.modal-backdrop-custom {
  position: fixed;
  inset: 0;
  z-index: 9999;
  background-color: rgba(0, 0, 0, 0.6);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
}

/* ── Header Styles ── */
.modal-header.ccardModalHead {
  padding: 1.25rem 1.5rem;
  border-bottom: 1px solid #e9ecef;
  background-color: var(--primary);
  border-radius: 12px 12px 0 0;
}

.modal-header .modal-title {
  margin: 0;
  font-size: 1.25rem;
  font-weight: 600;
  color: var(--white-color);
}

/* ── Footer Styles ── */
.modal-footer.ccardModalFoot {
  padding: 1rem 1.5rem;
  border-top: 1px solid #e9ecef;
  background-color: var(--primary);
  border-radius: 0 0 12px 12px;
  display: flex;
  justify-content: flex-end;
}

.modal-box {
  background-color: #fff;
  border-radius: 12px;
  max-width: 900px;
  width: 100%;
  max-height: 85vh;
  overflow-y: auto;
  box-shadow: 0 25px 80px rgba(0, 0, 0, 0.35);
  display: flex;
  flex-direction: column;
  z-index: 1700;
}

/* ── Modal Body Layout ── */
.modal-body.ccardModalBody {
  display: flex;
  flex-direction: row;
  gap: 1.5rem;
  padding: 1.5rem;
  align-items: flex-start;
}

/* ── Image Styles ── */
.modal-image-wrapper {
  flex-shrink: 0;
  width: 280px;
}

.modal-image {
  width: 100%;
  height: auto;
  border-radius: 10px;
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
  border: 3px solid #f0f0f0;
  object-fit: cover;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.modal-image:hover {
  transform: scale(1.02);
  box-shadow: 0 12px 35px rgba(0, 0, 0, 0.2);
}

/* Columna derecha: chip + descripción */
.modal-right-col {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
  padding: 0.5rem 0;
}

/* Chip de fecha */
.modal-date-chip {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 5px 12px;
  border-radius: 20px;
  background-color: rgba(var(--primary-rgb), 0.08);
  border: 1px solid rgba(var(--primary-rgb), 0.2);
  color: var(--primary);
  font-size: 0.8rem;
  font-weight: 500;
  width: fit-content;
  letter-spacing: 0.01em;
}

.modal-date-chip svg {
  flex-shrink: 0;
  opacity: 0.85;
}

/* Descripción (sin cambios funcionales) */
.modal-description {
  flex: 1;
  font-size: 1rem;
  line-height: 1.7;
  color: #444;
  text-align: justify;
}

/* ── Description Styles ── */
/* .modal-description {
  flex: 1;
  font-size: 1rem;
  line-height: 1.7;
  color: #444;
  text-align: justify;
  padding: 0.5rem 0;
} */

.modal-description :deep(p) {
  margin-bottom: 1rem;
}

.modal-description :deep(a) {
  color: #0d6efd;
  text-decoration: underline;
}

.modal-description :deep(strong),
.modal-description :deep(b) {
  color: #333;
}

/* ── Responsive: Mobile ── */
@media (max-width: 768px) {
  .modal-backdrop-custom {
    padding: 10px;
    align-items: flex-start;
    padding-top: 20px;
  }

  .modal-box {
    max-width: 100%;
    border-radius: 10px;
    max-height: 90vh;
  }

  .modal-header.ccardModalHead {
    padding: 1rem;
    border-radius: 10px 10px 0 0;
  }

  .modal-header .modal-title {
    font-size: 1.1rem;
  }

  .modal-body.ccardModalBody {
    flex-direction: column;
    align-items: center;
    padding: 1rem;
    gap: 1rem;
  }

  .modal-image-wrapper {
    width: 100%;
    max-width: 280px;
  }

  .modal-image {
    border-radius: 8px;
  }

  .modal-description {
    font-size: 0.95rem;
    text-align: left;
  }

  .modal-footer.ccardModalFoot {
    padding: 0.875rem 1rem;
    border-radius: 0 0 10px 10px;
  }
}

/* ── Responsive: Small Mobile ── */
@media (max-width: 480px) {
  .modal-backdrop-custom {
    padding: 8px;
  }

  .modal-header.ccardModalHead {
    padding: 0.875rem;
  }

  .modal-header .modal-title {
    font-size: 1rem;
  }

  .modal-body.ccardModalBody {
    padding: 0.875rem;
    gap: 0.875rem;
  }

  .modal-image-wrapper {
    max-width: 220px;
  }

  .modal-description {
    font-size: 0.9rem;
    line-height: 1.6;
  }

  .modal-footer.ccardModalFoot {
    padding: 0.75rem;
  }
}

/* ── Transition ── */
.modal-enter-active {
  transition: opacity 0.3s ease;
}

.modal-enter-active .modal-box {
  animation: modal-slide-in 0.3s ease forwards;
}

.modal-leave-active {
  transition: opacity 0.25s ease;
}

.modal-leave-active .modal-box {
  animation: modal-slide-out 0.25s ease forwards;
}

.modal-enter-from {
  opacity: 0;
}

.modal-leave-to {
  opacity: 0;
}

@keyframes modal-slide-in {
  from {
    opacity: 0;
    transform: translateY(30px) scale(0.95);
  }

  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

@keyframes modal-slide-out {
  from {
    opacity: 1;
    transform: translateY(0) scale(1);
  }

  to {
    opacity: 0;
    transform: translateY(20px) scale(0.97);
  }
}

.ccarda {
  background: transparent;
  border: 2px solid var(--border-light);
}
</style>
