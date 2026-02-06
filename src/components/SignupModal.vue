<script setup>
import { reactive, ref, watch, onBeforeUnmount } from 'vue'

const props = defineProps({
  show: Boolean,

  appsScriptUrl: {
    type: String,
    required: true
  }
})

const emit = defineEmits(['update:show', 'submitted'])

const submitting = ref(false)
const submitted = ref(false)
const serverMessage = ref('')

const form = reactive({
  name: '',
  email: '',
  phone: '',
  message: ''
})

const firstInput = ref(null)

const close = () => {
  emit('update:show', false)
}

const submit = async (e) => {
  e.preventDefault()

  if (!form.name || !form.email) {
    alert('Por favor informe nome e e-mail')
    return
  }

  if (!props.appsScriptUrl || !props.appsScriptUrl.endsWith('/exec')) {
    alert('URL do Apps Script inválida')
    return
  }

  submitting.value = true
  serverMessage.value = ''

  const payload = {
    nome: form.name,
    email: form.email,
    telefone: form.phone,
    mensagem: form.message
  }

  try {
    // Use a "simple" content type to avoid CORS preflight in browsers.
    // Apps Script can still read the raw POST body via e.postData.contents.
    const res = await fetch(props.appsScriptUrl, {
      method: 'POST',
      mode: 'cors',
      headers: {
        'Content-Type': 'text/plain;charset=UTF-8'
      },
      body: JSON.stringify(payload)
    })

    if (!res.ok) {
      const text = await res.text().catch(() => '')
      throw new Error(`HTTP ${res.status} - ${text}`)
    }

    // Try to parse JSON response. If parsing fails, fall back to text and
    // treat a 200 OK as success (Apps Script sometimes returns plain text).
    let data = null
    let textBody = null
    try {
      data = await res.json()
    } catch (err) {
      // not JSON — read raw text for diagnostics
      textBody = await res.text().catch(() => '')
      console.warn('Response not JSON, body:', textBody)
    }

    // Determine success: prefer explicit {success:true}, else accept 200 OK
    const successFromBody = data?.success === true
    if (!successFromBody && data && data.success === false) {
      // explicit failure from script
      throw new Error(data?.message || 'Falha ao salvar na planilha')
    }

    if (!successFromBody && !data) {
      // no JSON returned; but HTTP 200 — consider success, but surface textBody
      serverMessage.value = textBody ? String(textBody) : 'Enviado com sucesso.'
    } else if (successFromBody) {
      serverMessage.value = data.message || 'Enviado com sucesso 🎉'
    }

    submitted.value = true
    serverMessage.value = 'Enviado com sucesso 🎉'

    emit('submitted', { ...form })

    // limpa formulário
    form.name = ''
    form.email = ''
    form.phone = ''
    form.message = ''

    setTimeout(close, 900)

  } catch (err) {
    console.error(err)
    serverMessage.value = `Erro ao enviar: ${err.message}`
  } finally {
    submitting.value = false
  }
}

const onKey = (e) => {
  if (e.key === 'Escape') close()
}

// Formata valores de telefone (BR): aceita até 11 dígitos e formata como
// (##) ####-#### ou (##) #####-#### dependendo do tamanho.
const formatPhoneValue = (value) => {
  const digits = String(value || '').replace(/\D/g, '').slice(0, 11)
  if (!digits) return ''
  if (digits.length <= 2) return `(${digits}`
  if (digits.length <= 6) return `(${digits.slice(0,2)}) ${digits.slice(2)}`
  if (digits.length <= 10) return `(${digits.slice(0,2)}) ${digits.slice(2,6)}-${digits.slice(6)}`
  // 11 dígitos (DDD + 9xxxx-xxxx)
  return `(${digits.slice(0,2)}) ${digits.slice(2,7)}-${digits.slice(7)}`
}

const onPhoneInput = (e) => {
  // Usa o evento direto para pegar o valor bruto do input (inclui o cursor)
  const raw = e.target.value
  const formatted = formatPhoneValue(raw)
  form.phone = formatted
}

watch(() => props.show, (val) => {
  if (val) {
    setTimeout(() => firstInput.value?.focus(), 80)
    window.addEventListener('keydown', onKey)
  } else {
    window.removeEventListener('keydown', onKey)
    submitted.value = false
    serverMessage.value = ''
  }
})

onBeforeUnmount(() => {
  window.removeEventListener('keydown', onKey)
})
</script>

<template>
  <div v-if="props.show" class="modal-overlay" @click.self="close">
    <div class="modal" role="dialog" aria-modal="true" aria-label="Formulário de inscrição">
      <button class="modal-close" @click="close" aria-label="Fechar">×</button>
  <h3>Inscreva-se no <span class="brand-green">leveMente</span></h3>
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
          <input v-model="form.phone" @input="onPhoneInput" inputmode="tel" type="text" placeholder="(11) 9xxxx-xxxx" />
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
        <div v-if="serverMessage" class="server-message">{{ serverMessage }}</div>
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

.server-message {
  margin-top: 12px;
  font-size: 0.95rem;
  color: #065f46;
}

.brand-green {
  color: #16a34a; /* verde consistente com o tema */
  font-weight: 600;
}
</style>
