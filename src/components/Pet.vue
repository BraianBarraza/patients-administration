<script setup>
defineProps({
  pet:{
    type: Object,
    required: true
  }
})

defineEmits(['edit-patients', 'delete-patients'])
</script>

<template>
  <div class="mx-5 my-10 bg-white shadow-md px-5 py-10 rounded-xl">
    <p class="font-bold mb-3 text-gray-700 uppercase">ID:
      <span class="font-normal normal-case">
        {{ pet.id }}
            </span>
    </p>

    <p class="font-bold mb-3 text-gray-700 uppercase">Pet Name:
      <span class="font-normal normal-case">
        {{ pet.petName }}
            </span>
    </p>

    <p class="font-bold mb-3 text-gray-700 uppercase">Pet Owner:
      <span class="font-normal normal-case">
        {{ pet.petOwner }}
            </span>
    </p>

    <p class="font-bold mb-3 text-gray-700 uppercase">Cellphone :
      <span class="font-normal normal-case">
        {{ pet.cellphone }}
            </span>
    </p>

    <p class="font-bold mb-3 text-gray-700 uppercase">Email:
      <span class="font-normal normal-case">
        {{ pet.email }}
            </span>
    </p>

    <p class="font-bold mb-3 text-gray-700 uppercase">Discharge date:
      <span class="font-normal normal-case">
        {{ pet.discharge }}
            </span>
    </p>

    <p class="font-bold mb-3 text-gray-700 uppercase">Symptoms:
      <span class="font-normal normal-case">
        {{ pet.symptoms }}
            </span>
    </p>

    <div class="grid md:grid-cols-2  gap-5 mt-10 ">
      <button
          type="button"
          class="block w-full py-2 px-10 bg-indigo-600 hover:bg-indigo-700 text-white font-bold uppercase rounded-lg"
          @click.prevent="$emit('edit-patients', pet.id)"
      >Edit</button>

      <button
          type="button"
          class="block w-full py-2 px-10 bg-red-600 hover:bg-red-700 text-white font-bold uppercase rounded-lg"
          @click.prevent="$emit('delete-patients', pet.id)"
      >Delete</button>
    </div>
  </div>
</template>