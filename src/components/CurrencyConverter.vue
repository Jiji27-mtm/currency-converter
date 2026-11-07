<script setup>
import { ref } from 'vue'
import { devises, taux } from '../data/taux.js'

const montant = ref('0')
const deviseSource = ref('USD')
const deviseCible = ref('EUR')
const resultat = ref('')
const erreur = ref(false)

const touches = ['7', '8', '9', '4', '5', '6', '1', '2', '3', 'C', '0', '.']

function appuyer(touche) {
  erreur.value = false

  if (touche === 'C') {
    montant.value = '0'
    resultat.value = ''
  } else {
    if (montant.value.length >= 10) {
      return
    }
    if (touche === '.' && montant.value.includes('.')) {
      return
    }
    if (montant.value === '0' && touche !== '.') {
      montant.value = touche
    } else {
      montant.value = montant.value + touche
    }
  }
}

function convertir() {
  const nombre = parseFloat(montant.value)

  if (nombre === 0) {
    erreur.value = true
    resultat.value = ''
  } else {
    erreur.value = false
    const enEuro = nombre / taux[deviseSource.value]
    const final = enEuro * taux[deviseCible.value]
    resultat.value = final.toFixed(2)
  }
}

function inverser() {
  const temp = deviseSource.value
  deviseSource.value = deviseCible.value
  deviseCible.value = temp

  if (resultat.value !== '') {
    convertir()
  }
}
</script>

<template>
  <div class="carte">
    <div class="haut">
      <h1>Currency Converter</h1>

      <div class="ligne">
        <select v-model="deviseSource">
          <option v-for="d in devises" :key="d" :value="d">{{ d }}</option>
        </select>
        <div class="nombre">{{ montant }}</div>
      </div>

      <button class="btn-inverser" @click="inverser">⇅</button>

      <div class="ligne">
        <select v-model="deviseCible">
          <option v-for="d in devises" :key="d" :value="d">{{ d }}</option>
        </select>
        <div class="nombre">{{ resultat }}</div>
      </div>

      <button class="btn-convertir" @click="convertir">CONVERTIR</button>

      <p v-if="erreur">Veuillez saisir un montant</p>
    </div>

    <div class="clavier">
      <button
        v-for="t in touches"
        :key="t"
        :class="{ 'touche-effacer': t === 'C' }"
        @click="appuyer(t)"
      >
        {{ t }}
      </button>
    </div>
  </div>
</template>

<style scoped>
.carte {
  width: 100%;
  max-width: 360px;
  background-color: white;
  border-radius: 15px;
  overflow: hidden;
}

.haut {
  background-color: pink;
  padding: 20px;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

h1 {
  text-align: center;
  color: white;
  font-size: 20px;
  margin: 0;
}

.ligne {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
}

select {
  font-size: 16px;
  padding: 5px;
}

.nombre {
  color: white;
  font-size: 48px;
  text-align: right;
  border-bottom: 2px solid white;
  min-width: 150px;
  min-height: 56px;
}

.btn-inverser {
  background: none;
  border: none;
  color: white;
  font-size: 24px;
  width: 40px;
  cursor: pointer;
}

.btn-convertir {
  padding: 10px;
  border: none;
  border-radius: 20px;
  background-color: white;
  color: #1BA6C9;
  font-weight: bold;
  cursor: pointer;
}

p {
  color: white;
  text-align: center;
  margin: 0;
}

.clavier {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  padding: 15px;
}

.clavier button {
  background: none;
  border: none;
  font-size: 32px;
  color: pink;
  padding: 12px;
  cursor: pointer;
}

.touche-effacer {
  color: #F0727A ;
}
</style>