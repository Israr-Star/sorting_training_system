<!-- <script setup>
import { defineProps, defineEmits, ref, computed } from 'vue'

const modalVisible = ref(false)

const toggleModal = () => {
  modalVisible.value = !modalVisible.value
}

const emit = defineEmits(['close', 'start']) // Add update:isVisible

console.log(modalVisible, 'props.isVisible')
const peopleCount = ref(20) // Default value

const closeModal = () => {
  emit('close') // Emit event to close the modal
}

const startAction = () => {
  console.log(`Starting with ${peopleCount.value} people`)
  emit('start', peopleCount.value) // Emit event with input value
  closeModal()
}
const data = ref([
  {
    email: 'juozas@bybosas.lt',
    potatoes: 1,
    tags: ['Customers'],
    fullName: 'Juozas Bybosas',
    location: 'Lithuania',
    selected: false,
  },
  {
    email: 'john@smith.com',
    potatoes: 5,
    tags: ['Customers'],
    fullName: 'Gintare Peckyte',
    location: 'Lithuania',
    selected: false,
  },
  {
    email: 'gintare.peckyte@gmail.com',
    potatoes: 6,
    tags: ['Customers'],
    fullName: 'Gintare Peckyte',
    location: 'Lithuania',
    selected: false,
  },
  {
    email: 'gintare.peckyte@gmail.com',
    potatoes: 8,
    tags: ['Customers'],
    fullName: 'Gintare Peckyte',
    location: 'Lithuania',
    selected: true,
  },
  {
    email: 'gintare.peckyte@gmail.com',
    potatoes: 9,
    tags: ['Customers'],
    fullName: 'Gintare Peckyte',
    location: 'Lithuania',
    selected: false,
  },
  {
    email: 'kazka@gmail.com',
    potatoes: 4,
    tags: ['Customers'],
    fullName: 'Lorem Ipsum',
    location: 'Lithuania',
    selected: true,
  },
  {
    email: 'gintare.peckyte@gmail.com',
    potatoes: 2,
    tags: ['Customers', 'VIP'],
    fullName: 'Dolor Sit',
    location: 'Lithuania',
    selected: false,
  },
  {
    email: 'bbzbbd@gmail.com HOVER',
    potatoes: 7,
    tags: ['Customers'],
    fullName: 'Amet Bibendum',
    location: 'Lithuania',
    selected: false,
  },
  {
    email: 'rolandas.paksas@mail.ru',
    potatoes: 3,
    tags: ['Customers'],
    fullName: '',
    location: 'Lithuania',
    selected: false,
  },
  {
    email: 'gintare.peckyte@gmail.com',
    potatoes: 10,
    tags: ['Customers'],
    fullName: '',
    location: 'Lithuania',
    selected: false,
  },
  {
    email: 'gintare.peckyte@gmail.com',
    potatoes: 12,
    tags: ['Customers', 'Oldtimer'],
    fullName: '',
    location: 'Lithuania',
    selected: false,
  },
  {
    email: 'gintare.peckyte@gmail.com',
    potatoes: 11,
    tags: ['Customers'],
    fullName: '',
    location: 'Lithuania',
    selected: false,
  },
  {
    email: 'gintare.peckyte@gmail.com',
    potatoes: 13,
    tags: ['Customers'],
    fullName: '',
    location: 'Lithuania',
    selected: false,
  },
  {
    email: 'gintare.peckyte@gmail.com',
    potatoes: 7,
    tags: ['Customers', 'Oldtimer', '+1'],
    fullName: '',
    location: 'Lithuania',
    selected: false,
  },
])

const toggleSelect = (index) => {
  data.value[index].selected = !data.value[index].selected
}
</script> -->
<script setup lang="ts">
import { ref, computed } from 'vue'
interface Person {
  email: string
  potatoes: number
  tags: string[]
  fullName: string
  location: string
  selected: boolean
}
const modalVisible = ref(false)
const peopleCount = ref()

const toggleModal = () => {
  modalVisible.value = !modalVisible.value
}
console.log(peopleCount, 'peopleCount')
const peopleArray = computed(() => {
  const count = peopleCount.value
  if (count <= 0) {
    return [] // Return an empty array for non-positive counts
  }
  return Array.from({ length: count }, (_, index) => `Person ${index + 1}`)

  // Or if you just need an array of numbers:
  // return Array.from({ length: count }, (_, index) => index + 1);
})
const civilServants = ref<Person[]>([])

const data = ref([
  {
    email: 'juozas@bybosas.lt',
    potatoes: 1,
    tags: ['Customers'],
    fullName: 'Juozas Bybosas',
    location: 'Lithuania',
    selected: false,
  },
  {
    email: 'john@smith.com',
    potatoes: 5,
    tags: ['Customers'],
    fullName: 'Gintare Peckyte',
    location: 'Lithuania',
    selected: false,
  },
  {
    email: 'gintare.peckyte@gmail.com',
    potatoes: 6,
    tags: ['Customers'],
    fullName: 'Gintare Peckyte',
    location: 'Lithuania',
    selected: false,
  },
  {
    email: 'gintare.peckyte@gmail.com',
    potatoes: 8,
    tags: ['Customers'],
    fullName: 'Gintare Peckyte',
    location: 'Lithuania',
    selected: true,
  },
  {
    email: 'gintare.peckyte@gmail.com',
    potatoes: 9,
    tags: ['Customers'],
    fullName: 'Gintare Peckyte',
    location: 'Lithuania',
    selected: false,
  },
  {
    email: 'kazka@gmail.com',
    potatoes: 4,
    tags: ['Customers'],
    fullName: 'Lorem Ipsum',
    location: 'Lithuania',
    selected: true,
  },
  {
    email: 'gintare.peckyte@gmail.com',
    potatoes: 2,
    tags: ['Customers', 'VIP'],
    fullName: 'Dolor Sit',
    location: 'Lithuania',
    selected: false,
  },
  {
    email: 'bbzbbd@gmail.com HOVER',
    potatoes: 7,
    tags: ['Customers'],
    fullName: 'Amet Bibendum',
    location: 'Lithuania',
    selected: false,
  },
  {
    email: 'rolandas.paksas@mail.ru',
    potatoes: 3,
    tags: ['Customers'],
    fullName: '',
    location: 'Lithuania',
    selected: false,
  },
  {
    email: 'gintare.peckyte@gmail.com',
    potatoes: 10,
    tags: ['Customers'],
    fullName: '',
    location: 'Lithuania',
    selected: false,
  },
  {
    email: 'gintare.peckyte@gmail.com',
    potatoes: 12,
    tags: ['Customers', 'Oldtimer'],
    fullName: '',
    location: 'Lithuania',
    selected: false,
  },
  {
    email: 'gintare.peckyte@gmail.com',
    potatoes: 11,
    tags: ['Customers'],
    fullName: '',
    location: 'Lithuania',
    selected: false,
  },
  {
    email: 'gintare.peckyte@gmail.com',
    potatoes: 13,
    tags: ['Customers'],
    fullName: '',
    location: 'Lithuania',
    selected: false,
  },
  {
    email: 'gintare.peckyte@gmail.com',
    potatoes: 7,
    tags: ['Customers', 'Oldtimer', '+1'],
    fullName: '',
    location: 'Lithuania',
    selected: false,
  },
])

//code started for table generate

const generateRandomName = (): string => {
  const firstNames = [
    'John',
    'Jane',
    'Alex',
    'Emily',
    'Chris',
    'Katie',
    'Mark',
    'Sarah',
    'Michael',
    'Jessica',
  ]
  const lastNames = [
    'Smith',
    'Johnson',
    'Brown',
    'Taylor',
    'Anderson',
    'Lee',
    'Clark',
    'Harris',
    'Lewis',
    'Walker',
  ]

  const firstName = firstNames[Math.floor(Math.random() * firstNames.length)]
  const lastName = lastNames[Math.floor(Math.random() * lastNames.length)]

  return `${firstName} ${lastName}`
}

const generateRandomEmail = (name: string, id: number): string => {
  const domains = ['gmail.com', 'yahoo.com', 'outlook.com', 'hotmail.com']
  const emailDomain = domains[Math.floor(Math.random() * domains.length)]
  const nameParts = name.toLowerCase().split(' ')
  const username = `${nameParts[0]}.${nameParts[1] + id}`

  return `${username}@${emailDomain}`
}

const shuffleArray = (arr: number[]): void => {
  for (let i = arr.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1))
    ;[arr[i], arr[j]] = [arr[j], arr[i]]
  }
}
const generateData = (): Person[] => {
  const peopleData: Person[] = []
  const potatoNumbers: number[] = Array.from(
    { length: 1000 },
    (_, index) => index + 1,
  )

  shuffleArray(potatoNumbers)

  for (let i = 0; i < peopleCount.value; i++) {
    const fullName = generateRandomName()
    const email = generateRandomEmail(fullName, i)
    const potatoes = potatoNumbers[i]
    const location = 'Lithuania'
    const tags = ['Customers']
    const selected = false

    peopleData.push({ email, potatoes, tags, fullName, location, selected })
  }
  console.log(peopleData, peopleCount, 'peopleCount')
  return peopleData
}
const handleStart = (count) => {
  console.log('Start action in parent with count:', count)
  civilServants.value = generateData()
  // ... your logic for handling the start action
}
</script>
<template>
  <div class="m-[60px]">
    <div class="flex items-center justify-between">
      <h1 class="text-4xl font-bold leading-[37.5px] text-left text-black">
        Sorting Training System
      </h1>
      <button
        class="w-[161px] h-[50px] rounded-[5px] bg-[#FF8D00] text-white cursor-pointer"
        @click="toggleModal"
      >
        Start Sorting
      </button>
    </div>
    <div
      class="mt-[42px] rounded-[5px] border border-[#DDDDDD] shadow-[0px_0px_4px_0px_#0000001A]"
    >
      <p class="text-right m-[20px]">{{ peopleCount }} people in the list</p>
      <div class="bg-white shadow-lg rounded-lg">
        <table class="min-w-full border-collapse border border-[#DDDDDD]">
          <thead>
            <tr class="text-[#555555] text-sm leading-[18px] text-left">
              <th class="px-[20px] py-[15px] font-normal">
                Email
              </th>
              <th
                class="p-[15px] font-normal border-l border-[#DDDDDD] pl-[40px]"
              >
                Potatoes
              </th>
              <th class="p-[15px] font-normal">
                Tags
              </th>
              <th class="p-[15px] font-normal">
                Full Name
              </th>
              <th class="p-[15px] font-normal">
                Location
              </th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="(row, index) in civilServants"
              :key="index"
              :class="row.selected ? 'bg-gray-100' : ''"
              class="border border-[#DDDDDD] hover:bg-gray-50 text-sm font-normal leading-[18px] text-left text-[#000000]"
            >
              <td class="p-3 flex items-center gap-2 px-[20px]">
                <input
                  type="checkbox"
                  :checked="row.selected"
                  @change="toggleSelect(index)"
                  class="form-checkbox h-4 w-4 text-orange-500 border-gray-300 rounded"
                />
                {{ row.email }}
              </td>
              <td class="p-3 border-l border-[#DDDDDD] pl-[40px]">
                {{ row.potatoes }}
              </td>
              <td class="p-3 flex gap-1">
                <span
                  v-for="(tag, i) in row.tags"
                  :key="i"
                  class="px-2 py-1 text-sm bg-gray-200 rounded-lg"
                >
                  {{ tag }}
                </span>
              </td>
              <td class="p-3">{{ row.fullName }}</td>
              <td class="p-3">{{ row.location }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>

  <div
    v-if="modalVisible"
    class="fixed inset-0 flex items-center justify-center bg-opacity-20"
  >
    <div class="bg-white rounded-lg shadow-lg p-6 w-96">
      <!-- Header -->
      <div class="flex justify-between items-center">
        <h2 class="text-lg font-bold">How many people?</h2>
        <button
          @click="toggleModal"
          class="text-gray-500 hover:text-gray-700 text-xl"
        >
          &times;
        </button>
      </div>

      <!-- Description -->
      <p class="text-gray-600 mt-2 text-sm">
        Enter a number of how many people you want to add to the list.
      </p>

      <!-- Input Field -->
      <input
        v-model.number="peopleCount"
        type="number"
        class="mt-4 w-full px-3 py-2 border rounded-md focus:ring-2 focus:ring-orange-500 focus:border-orange-500"
        placeholder="Enter a number"
      />
      <!-- <p>People Count: {{ peopleCount }}</p>
      <p>People Array: {{ civilServants }}</p> -->
      <!-- Buttons -->
      <div class="mt-6 flex justify-end space-x-2">
        <button
          @click="toggleModal"
          class="px-4 py-2 text-gray-700 border rounded-md hover:bg-gray-100"
        >
          Cancel
        </button>
        <button
          @click="handleStart"
          class="px-4 py-2 bg-orange-500 text-white rounded-md hover:bg-orange-600"
        >
          Start
        </button>
      </div>
    </div>
  </div>
</template>
