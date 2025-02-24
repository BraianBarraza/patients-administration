<script setup>
  import {reactive, computed} from 'vue'
  import Alert from './Alert.vue';

  const alert = reactive({
    message: '',
    alertType: ''
  })

  const emit = defineEmits([
    'update:pet-name',
    'update:pet-owner',
    'update:cellphone',
    'update:email',
    'update:discharge',
    'update:symptoms',
    'save-patients'
  ])

  const props = defineProps({
    id:{
      type:[String, null],
      required:true
    },
    petName:{
      type:String,
      required:true
    },
    petOwner:{
      type:String,
      required:true
    },
    cellphone:{
      type:Number,
      required:true
    },
    email:{
      type:String,
      required:true
    },
    discharge:{
      type:String,
      required:true
    },
    symptoms:{
      type:String,
      required:true
    }
  })

  const validation = () => {
    if (Object.values(props).includes('')){
      alert.message = 'Please fill all fields'
      alert.alertType = 'error'
      return
    }

    emit('save-patients')
    alert.message = 'Pet added successfully'
    alert.alertType = 'success'

    setTimeout(()=>{
      Object.assign(alert,{
        message: '',
        alertType: ''
      })
    },3000)
  }

  const editing = computed(()=>{
    return props.id
  })

</script>

<template>
    <div class="md:w-1/2">
        <h2 class="font-black text-3xl text-center">
            Monitoring
        </h2>

        <p class="text-lg mt-5 text-center mb-10">
            Add patients &
            <span class="text-indigo-600 font-bold">Manage them</span>
        </p>

      <Alert v-if="alert.message" :alert="alert" />

      <form
          class="bg-white shadow-md rounded-lg px-5 py-10 mb-10"
      >
        <div class="mb-5">
          <label for="petName"
            class="block text-gray-700 uppercase font-bold">
            Pet name
          </label>
          <input type="text"
                 id="petName"
                 placeholder="Pet name"
                 class="border-1 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                 :value="petName"
                 @input="$emit('update:pet-name', $event.target.value)"
          />
        </div>

        <div class="mb-5">
          <label for="petOwner"
                 class="block text-gray-700 uppercase font-bold">
            Pet owner name
          </label>
          <input type="text"
                 id="petOwner"
                 placeholder="Pet owner name"
                 class="border-1 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                 :value="petOwner"
                 @input="$emit('update:pet-owner', $event.target.value)"
          />
        </div>

        <div class="mb-5">
          <label for="telephone"
                 class="block text-gray-700 uppercase font-bold">
            Cellphone
          </label>
          <input type="text"
                 id="petOwner"
                 placeholder="Cellphone number"
                 class="border-1 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                 :value="cellphone"
                 @input="$emit('update:cellphone', $event.target.value)"
          />
        </div>

        <div class="mb-5">
          <label for="email"
                 class="block text-gray-700 uppercase font-bold">
            E-mail
          </label>
          <input type="email"
                 id="email"
                 placeholder="E-mail"
                 class="border-1 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                 :value="email"
                 @input="$emit('update:email', $event.target.value)"/>
        </div>

        <div class="mb-5">
          <label for="discharge"
                 class="block text-gray-700 uppercase font-bold">
            Medical Discharge Date
          </label>
          <input type="date"
                 id="discharge"
                 class="border-1 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                 :value="discharge"
                 @input="$emit('update:discharge', $event.target.value)"/>
        </div>

        <div class="mb-5">
          <label for="symptoms"
                 class="block text-gray-700 uppercase font-bold">
            Symptoms
          </label>
          <textarea
                 id="symptoms"
                 placeholder="Symptoms description"
                 class="border-1 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                 :value="symptoms"
                 @input="$emit('update:symptoms', $event.target.value)"/>
        </div>

        <input type="submit"
               class="bg-indigo-600 w-full text-white font-bold py-2 px-4 rounded-md hover:bg-indigo-500 cursor-pointer
               transition-colors"
               :value="[editing ? 'Save changes' : 'Add new Patient']"
               v-on:click.prevent="validation"/>
      </form>
    </div>
</template>


