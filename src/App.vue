<script setup>
import { ref, computed } from 'vue'
const numero1 = ref('')
const numero2 = ref('')
const selectedOps = ref({
  somar: true,
  subtrair: false,
  multiplicar: false,
  dividir: false,
})
function toggle(op) {
  Object.keys(selectedOps.value).forEach(k => {
    selectedOps.value[k] = false
  })
  selectedOps.value[op] = true
}
const resultado = computed(() => {
  const a = parseFloat(numero1.value)
  const b = parseFloat(numero2.value)
  if (isNaN(a) || isNaN(b)) return ''
  if (selectedOps.value.somar) return a + b
  if (selectedOps.value.subtrair) return a - b
  if (selectedOps.value.multiplicar) return a * b
  if (selectedOps.value.dividir) return b === 0 ? 'Erro: divisão por 0' : a / b
  return ''
})
</script>

<template>
  <header class="container calculadora">
    <div class="p-5 mb-4 rounded-3 mt-5">
      <h1>Calculadora</h1>
      <h2>Desenvolvida por: Felipe</h2>
    </div>
    <hr>
    <form @submit.prevent class="p-5 mb-4 rounded-3 mt-5">
      <div class="row g-3 align-items-center">
        <div class="col">
          <input type="number" class="form-control" placeholder="Número 1" v-model="numero1"/>
        </div>

        <div class="col-auto">
          <div class="row gx-2">
            <div class="col">
              <ul class="list-group">
                <li class="list-group-item d-flex align-items-center">
                  <input type="checkbox" :checked="selectedOps.somar" @change="toggle('somar')" />
                  <label class="ms-2 mb-0">Somar</label>
                </li>
                <li class="list-group-item d-flex align-items-center">
                  <input type="checkbox" :checked="selectedOps.subtrair" @change="toggle('subtrair')" />
                  <label class="ms-2 mb-0">Subtrair</label>
                </li>
              </ul>
            </div>
            <div class="col">
              <ul class="list-group">
                <li class="list-group-item d-flex align-items-center">
                  <input type="checkbox" :checked="selectedOps.multiplicar" @change="toggle('multiplicar')" />
                  <label class="ms-2 mb-0">Multiplicar</label>
                </li>
                <li class="list-group-item d-flex align-items-center">
                  <input type="checkbox" :checked="selectedOps.dividir" @change="toggle('dividir')" />
                  <label class="ms-2 mb-0">Dividir</label>
                </li>
              </ul>
            </div>
          </div>
        </div>

        <div class="col">
          <input type="number" class="form-control" placeholder="Número 2" v-model="numero2"/>
        </div>

        <div class="col">
          <h3>Resultado: {{ resultado !== '' ? resultado : '—' }}</h3>
        </div>
      </div>
    </form>
  </header>
</template>

<style scoped>
.calculadora {
  background-color: #dfd493;
  border-radius: 10px;
  text-align: center;
  color: black;
}
</style>
