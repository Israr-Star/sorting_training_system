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
import { ref, computed, onMounted, onUnmounted, watch } from 'vue'
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
  toggleModal()
  return peopleData
}
const handleStart = (count) => {
  console.log('Start action in parent with count:', count)
  civilServants.value = generateData()
  // ... your logic for handling the start action
}
const timer = ref(0)
const isSorted = ref(false)
const draggedIndex = ref<number | null>(null)
let interval: number | null = null

const isDataSorted = (people: Person[]): boolean => {
  return people.every(
    (_, i, arr) => i === 0 || arr[i - 1].potatoes >= arr[i].potatoes,
  )
}

// onMounted(() => {
//   if (isDataSorted(civilServants?.value)) {
//     interval = setInterval(() => {
//       timer.value++
//     }, 1000)
//   }
// })
watch(civilServants, (newVal) => {
  console.log(newVal.length, isDataSorted(newVal), 'newVal')
  if (newVal.length && !isDataSorted(newVal)) {
    // Start Timer
    interval = setInterval(() => {
      timer.value += 1
    }, 1000)
  } else {
    // Stop Timer if data is sorted
    clearInterval(interval)
    timer.value = 0
  }
})

onUnmounted(() => {
  if (interval) clearInterval(interval)
})

const handleDragStart = (index: number) => {
  draggedIndex.value = index
}

const handleDragOver = (event: DragEvent) => {
  event.preventDefault()
}

const handleDrop = (index: number) => {
  if (draggedIndex.value === null || draggedIndex.value === index) return

  const updatedPeople = [...civilServants?.value]
  const [draggedItem] = updatedPeople.splice(draggedIndex.value, 1)
  updatedPeople.splice(index, 0, draggedItem)

  if (isDataSorted(updatedPeople)) {
    isSorted.value = true
    alert(`Sorted! Timer stopped at ${timer.value} seconds.`)
    timer.value = 0
    if (interval) clearInterval(interval)
  }

  civilServants.value = updatedPeople
  draggedIndex.value = null
}
</script>
<template>
  <div class="m-[60px]">
    <div class="flex items-center justify-between">
      <h1 class="text-4xl font-bold leading-[37.5px] text-left text-black">
        Sorting Training System
      </h1>
      <div v-if="timer > 0">
        Please start sorting. Your time started..
        {{ Math.floor(timer / 3600) }}h {{ Math.floor((timer % 3600) / 60) }}m
        {{ timer % 60 }}s
      </div>
      <div v-else>
        Congratulations! Table is sorted!
      </div>
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
              :key="row.id"
              :class="row.selected ? 'bg-gray-100' : ''"
              class="border border-[#DDDDDD] hover:bg-gray-50 text-sm font-normal leading-[18px] text-left text-[#000000]"
              :draggable="true"
              @dragstart="handleDragStart(index)"
              @dragover="handleDragOver"
              @drop="handleDrop(index)"
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
    class="fixed inset-0 flex items-center justify-center bg-opacity-40 bg-[rgba(0,0,0,0.5)]"
  >
    <div class="bg-white rounded-lg shadow-lg w-[437px] h-[280px]">
      <!-- Header -->
      <div
        class="flex justify-between items-center border-b border-[#CCCCCC] p-[20px]"
      >
        <h2 class="text-[14px] font-bold leading-[22px]">How many people?</h2>
        <!-- <button
          @click="toggleModal"
          class="text-gray-500 hover:text-gray-700 text-xl"
        >
          &times;
        </button> -->
        <svg
          width="12"
          height="12"
          viewBox="0 0 12 12"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
          xmlns:xlink="http://www.w3.org/1999/xlink"
          @click="toggleModal"
          class="cursor-pointer"
        >
          <rect width="12" height="12" fill="url(#pattern0_101_7)" />
          <mask
            id="mask0_101_7"
            style="mask-type: alpha;"
            maskUnits="userSpaceOnUse"
            x="0"
            y="0"
            width="12"
            height="12"
          >
            <rect width="12" height="12" fill="url(#pattern1_101_7)" />
          </mask>
          <g mask="url(#mask0_101_7)">
            <rect width="12" height="12" fill="#999999" />
          </g>
          <defs>
            <pattern
              id="pattern0_101_7"
              patternContentUnits="objectBoundingBox"
              width="1"
              height="1"
            >
              <use xlink:href="#image0_101_7" transform="scale(0.0078125)" />
            </pattern>
            <pattern
              id="pattern1_101_7"
              patternContentUnits="objectBoundingBox"
              width="1"
              height="1"
            >
              <use xlink:href="#image0_101_7" transform="scale(0.0078125)" />
            </pattern>
            <image
              id="image0_101_7"
              width="128"
              height="128"
              xlink:href="data:image/png;base64,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"
            />
          </defs>
        </svg>
      </div>

      <!-- Description -->
      <div class="px-[20px] pt-[20px] h-[150px] border-b border-[#CCCCCC]">
        <p class="text-[#555555] text-[13px] font-normal leading-[18px]">
          Enter a number of how many people you want to add to the list.
        </p>

        <input
          v-model.number="peopleCount"
          type="number"
          class="mt-4 w-full px-3 py-2 border border-[#CCCCCC] rounded-[5px] focus:border-transparent focus:ring-2 focus:ring-[#FF8D00] outline-none"
          placeholder="Enter a number between 20 and 100"
        />
        <p
          v-if="peopleCount < 20 || peopleCount > 100"
          class="text-red-500 text-sm pt-[6px]"
        >
          Please enter a number between 20 and 100
        </p>
      </div>
      <!-- <p>People Count: {{ peopleCount }}</p>
      <p>People Array: {{ civilServants }}</p> -->
      <!-- Buttons -->
      <div class="flex justify-end space-x-2 py-[20px] pr-[20px]">
        <button
          @click="toggleModal"
          class="px-4 py-2 text-[#555555] rounded-md border border-transparent hover:border-[#555555] text-[14px] font-bold leading-[16.41px] bg-gray-100 cursor-pointer"
        >
          Cancel
        </button>
        <button
          @click="handleStart"
          :disabled="peopleCount < 20 || peopleCount > 100"
          class="px-4 py-2 bg-orange-500 text-white rounded-md hover:bg-orange-600 disabled:opacity-50 text-[14px] font-bold leading-[16.41px] cursor-pointer"
        >
          Start
        </button>
      </div>
    </div>
  </div>
</template>
