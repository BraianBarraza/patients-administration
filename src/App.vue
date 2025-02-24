<script setup>
import {ref, reactive, watch, onMounted } from "vue";
import {uid} from "uid";
import Header from './components/Header.vue'
import Form from './components/Form.vue'
import Pet from "./components/Pet.vue";


const pets = ref([])

const pet = reactive({
  id: null,
  petName: '',
  petOwner: '',
  cellphone: '',
  email: '',
  discharge: '',
  symptoms: ''
})
watch(pets, ()=>{
  saveLocalStorage()
},{
  deep: true
})
const saveLocalStorage = () =>{
  localStorage.setItem('pets', JSON.stringify(pets.value))
}

onMounted(()=>{
  const localStoragePets = localStorage.getItem('pets')
  if(localStoragePets){
    pets.value = JSON.parse(localStoragePets)
  }
})

const savePatients = () => {
  if (pet.id){
    const {id} = pet
    const i = pets.value.findIndex((petState)=> petState.id === id)
    pets.value[i] = {...pet}
  }else{
    pets.value.push({
    ...pet, //Spread operator se utiliza para quitar a reactividad
    id: uid()
    })
  }


  Object.assign(pet, {
    petName: '',
    petOwner: '',
    cellphone: '',
    email: '',
    discharge: '',
    symptoms: '',
    id: null
  })
}

const editPatients = (id)=> {
  const patientInfo = pets.value.filter(pet => pet.id === id)[0]
  Object.assign(pet, patientInfo)
}
const deletePatients = (id)=> {
  pets.value = pets.value.filter(pet => pet.id !== id)
}
</script>

<template>
  <div class="container mx-auto mt-20">
    <Header />

    <div class="mt-12 md:flex" >
      <Form
      v-model:petName="pet.petName"
      v-model:petOwner="pet.petOwner"
      v-model:cellphone="pet.cellphone"
      v-model:email="pet.email"
      v-model:discharge="pet.discharge"
      v-model:symptoms="pet.symptoms"
      v-model:id="pet.id"
      @save-patients="savePatients"
      />

      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">
          Patients Management
        </h3>

        <div v-if="pets.length > 0">
          <p class="text-lg mt-5 text-center mb-10">
            Pets
            <span class="text-indigo-600 font-bold">information</span>
          </p>
          <Pet v-for="pet in pets"
               :pet="pet"
               @edit-patients = "editPatients"
               @delete-patients = "deletePatients"
          />
        </div>

        <div v-else>
          <p class="text-center mt-20 text-2xl font-black">
            There are no Patients
          </p>
        </div>

      </div>
    </div>
  </div>

 
</template>
