<script setup>
import { reactive, ref, watch, onMounted, onBeforeUnmount } from 'vue'

const props = defineProps({ show: Boolean })
const emit = defineEmits(['update:show', 'submitted'])

const submitting = ref(false)
const submitted = ref(false)
const form = reactive({ name: '', email: '', phone: '', message: '' })
const firstInput = ref(null)

const close = () => {
  emit('update:show', false)
}

const submit = async (e) => {
  e && e.preventDefault()
  if (!form.name || !form.email) {
    alert('Por favor informe nome e e-mail')
    return
  }
  submitting.value = true
  await new Promise((r) => setTimeout(r, 800))
  submitting.value = false
  submitted.value = true
  // emit data to parent
  emit('submitted', { ...form })
  // clear
  form.name = ''
  form.email = ''
  form.phone = ''
  form.message = ''
  // close after short delay to show success
  setTimeout(() => close(), 900)
}

const onKey = (e) => {
  if (e.key === 'Escape') close()
}

watch(() => props.show, (val) => {
  if (val) {
    // small delay to ensure element rendered
    setTimeout(() => firstInput.value && firstInput.value.focus(), 80)
    window.addEventListener('keydown', onKey)
  } else {
    window.removeEventListener('keydown', onKey)
    submitting.value = false
    submitted.value = false
  }
})

onMounted(() => {})
onBeforeUnmount(() => window.removeEventListener('keydown', onKey))
</script>

<template>
  <div v-if="props.show" class="modal-overlay" @click.self="close">
    <div class="modal" role="dialog" aria-modal="true" aria-label="Formulário de inscrição">
      <button class="modal-close" @click="close" aria-label="Fechar">×</button>
      <h3>Inscreva-se no LeveMENTE</h3>
      <p>Preencha o formulário para receber informações e começar sua jornada.</p>
      <form class="signup-form" @submit="submit">
        <label>
          Nome
          <input ref="firstInput" v-model="form.name" type="text" placeholder="Seu nome" required />
        </label>
        <label>
          Email
          <input v-model="form.email" type="email" placeholder="seu@exemplo.com" required />
        </label>
        <label>
          Telefone
          <input v-model="form.phone" type="text" placeholder="(11) 9xxxx-xxxx" />
        </label>
        <label>
          Mensagem (opcional)
          <textarea v-model="form.message" rows="4" placeholder="Alguma informação adicional"></textarea>
        </label>

        <div class="modal-actions">
          <button type="submit" class="btn-primary" :disabled="submitting">{{ submitting ? 'Enviando…' : 'Enviar inscrição' }}</button>
          <button type="button" class="btn-secondary" @click="close">Cancelar</button>
        </div>

        <div v-if="submitted" class="signup-success">Obrigado! Sua inscrição foi recebida.</div>
      </form>
    </div>
  </div>
</template>

<style scoped>
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(2,6,23,0.6);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 2000;
  padding: 24px;
}

.modal {
  background: white;
  width: 100%;
  max-width: 640px;
  border-radius: 12px;
  padding: 28px;
  box-shadow: 0 30px 60px rgba(2,6,23,0.3);
  position: relative;
}

.modal-close {
  position: absolute;
  top: 12px;
  right: 12px;
  background: transparent;
  border: none;
  font-size: 22px;
  cursor: pointer;
}

.signup-form {
  display: grid;
  gap: 12px;
  margin-top: 8px;
}

.signup-form label {
  display: flex;
  flex-direction: column;
  font-size: 0.95rem;
  color: #334155;
}

.signup-form input,
.signup-form textarea {
  margin-top: 8px;
  padding: 10px 12px;
  border-radius: 8px;
  border: 1px solid #e6eef3;
  background: #fbfdfe;
  font-size: 0.95rem;
}

.modal-actions {
  display: flex;
  gap: 12px;
  margin-top: 8px;
}

.signup-success {
  margin-top: 12px;
  color: #065f46;
  font-weight: 600;
}

.btn-primary {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 12px 24px;
  border-radius: 8px;
  font-weight: 500;
  text-decoration: none;
  border: none;
  cursor: pointer;
  transition: all 0.2s ease;
  font-size: 16px;
  background: linear-gradient(135deg, #22c55e 0%, #065f46 100%);
  color: white;
  box-shadow: 0 4px 14px 0 rgba(22, 163, 74, 0.25);
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 25px 0 rgba(22, 163, 74, 0.35);
}

.btn-secondary {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 12px 24px;
  border-radius: 8px;
  font-weight: 500;
  text-decoration: none;
  border: 2px solid #16a34a;
  background: transparent;
  color: #16a34a;
  cursor: pointer;
  transition: all 0.2s ease;
  font-size: 16px;
}

.btn-secondary:hover {
  background: #16a34a;
  color: white;
}
</style>
