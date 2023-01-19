<script setup>
</script>

<template>
 <!-- formulaire pour convertir un montant d'une monnaie à une autre -->
  <form @submit.prevent="convertir">
    <div class="form-group">
      <label for="montant">Montant</label>
      <input type="number" id="montant" v-model="montant" class="form-control" placeholder="Entrez un montant">
    </div>

     <div class="form-group">
        <label for="deviseDepart">Devise de départ</label>
        <select id="deviseDepart" v-model="deviseDepart" class="form-control">
        
          <option v-for="(devise, index) in devises" :value="devise" :key="index">{{ devise }}</option>
        </select>
      </div>

      <div class="form-group">
        <label for="deviseArrivee">Devise d'arrivée</label>
        <select id="deviseArrivee" v-model="deviseArrivee" class="form-control">
          <option v-for="(devise, index) in devises" :value="devise" :key="index">{{ devise }}</option>
          
        
        </select>
      </div>

      <button type="submit" class="btn btn-primary">Convertir</button>
  </form>

  <!-- resultslot le result correspond à result.value -->
</template>

<script>
import { ref, onMounted } from 'vue'
import axios from 'axios'

export default {
  name: 'HomeView',
  setup() {
    // Créez des références pour les devises, la devise de départ, la devise d'arrivée et le montant
    const devises = ref([])
    const deviseDepart = ref('')
    const deviseArrivee = ref('')
    const montant = ref(0)
    const result = ref(0)
    const deviseFull = ref('')

    // Utilisez onMounted pour appeler l'API lorsque le composant est monté
    onMounted(async () => {
      // Utilisez axios pour appeler l'API et récupérer les devises
      const response = await axios.get('https://api.frankfurter.app/currencies')
      // Mettez à jour la référence des devises avec les devises récupérées en index
      devises.value = Object.keys(response.data)
      

     

    })

    const convertir = async () => {
      // appeler l'api pour convertir le montant
      const response = await axios.get(`https://api.frankfurter.app/latest?amount=${montant.value}&from=${deviseDepart.value}&to=${deviseArrivee.value}`)
      // mettre à jour le résultat
      // calculer le résultat en fonction du montant, de la devise de départ et de la devise d'arrivée
      result.value = response.data.rates[deviseArrivee.value]
      console.log(result.value)



}
return {
  devises,
  deviseDepart,
  deviseArrivee,
  montant,
  result,
  convertir
}
}
}

</script>


<style scoped>

</style>
