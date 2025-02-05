<script setup lang="ts">
import { ref, onUnmounted } from 'vue'
import Header from './header.vue'

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
const finalScore = ref()

const toggleModal = () => {
  modalVisible.value = !modalVisible.value
}
console.log(peopleCount, 'peopleCount')

const civilServants = ref<Person[]>([])

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

const shuffleArray = (arr: number[] | Person[]): void => {
  for (let i = arr.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1))
    ;[arr[i], arr[j]] = [arr[j], arr[i]]
  }
  return arr
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
const resultShown = ref(false)
const handleStart = (count) => {
  if (resultShown.value) {
    // const arr = [...civilServants.value]
    // civilServants.value = shuffleArray(arr)
    civilServants.value = shuffleArray([...civilServants.value])
    resultShown.value = false
    isSorted.value = false
    toggleModal()

    interval = setInterval(() => {
      timer.value++
    }, 1000)
  } else {
    if (civilServants.value.length) {
      toggleModal()
      if (isSorted.value) {
        timer.value = 0
        resultShown.value = true
      } else {
        interval = setInterval(() => {
          timer.value++
        }, 1000)
      }
    } else {
      civilServants.value = generateData()
    }
  }
  // ... your logic for handling the start action
}
const timer = ref(0)
const isSorted = ref(false)
const draggedIndex = ref<number | null>(null)
let interval: ReturnType<typeof setInterval> | null = null

const isDataSorted = (people: Person[]): boolean => {
  return people.every(
    (_, i, arr) => i === 0 || arr[i - 1].potatoes >= arr[i].potatoes,
  )
}

// onMounted(() => {
//   if (civilServants.value.length && !isDataSorted(civilServants.value)) {
//     interval = setInterval(() => {
//       timer.value++
//     }, 1000)
//   }
// })
// watch(civilServants, (newVal) => {
//   console.log(newVal.length, isDataSorted(newVal), 'newVal')
//   if (newVal.length && !isDataSorted(newVal)) {
//     // Start Timer
//     interval = setInterval(() => {
//       timer.value += 1
//     }, 1000)
//   } else {
//     // Stop Timer if data is sorted
//     if (interval !== null) {
//       clearInterval(interval)
//     }
//     timer.value = 0
//   }
// })
const draggedItem = ref<Person | null>(null)
onUnmounted(() => {
  if (interval) clearInterval(interval)
})

const handleDragStart = (index: number) => {
  if (!isSorted.value) {
    draggedIndex.value = index
    draggedItem.value = civilServants.value[index]
    setTimeout(() => {
      civilServants.value.splice(index, 1)
    }, 0)
  }
}

const handleDragOver = (event: DragEvent) => {
  if (!isSorted.value) {
    event.preventDefault()
  }
}

const handleDrop = (index: number) => {
  if (
    (!isSorted.value && draggedIndex.value === null) ||
    draggedIndex.value === index
  )
    return

  if (draggedIndex.value === null || draggedIndex.value === index) return

  const updatedPeople = [...civilServants.value]
  if (draggedItem.value) {
    updatedPeople.splice(index, 0, draggedItem.value)
  }
  if (isDataSorted(updatedPeople)) {
    isSorted.value = true
    toggleModal()
    finalScore.value = (peopleCount.value / timer.value) * 100
    if (interval) clearInterval(interval)
  }

  civilServants.value = updatedPeople
  draggedIndex.value = null
  draggedItem.value = null
}
const handleDragEnd = () => {
  if (draggedItem?.value !== null && draggedIndex.value !== null) {
    civilServants.value.splice(draggedIndex.value, 0, draggedItem.value)
  }
  draggedIndex.value = null
  draggedItem.value = null
}

// const handleDeleteAll = () => {//future implementation
//   if (interval) clearInterval(interval)
//   civilServants.value = []
//   peopleCount.value = null
//   timer.value = 0
//   isSorted.value = false
//   resultShown.value = false
//   finalScore.value = 0
// }
</script>
<template>
  <div class="m-[60px]">
    {{ timer }}
    <Header
      :timer="timer"
      :civilServants="civilServants"
      @start-sorting="toggleModal"
    />
    <div
      class="mt-[42px] rounded-[5px] border border-[#DDDDDD] shadow-[0px_0px_4px_0px_#0000001A]"
    >
      <!-- <button
        class="px-2.5 py-2 text-[14px] rounded-[5px] border border-[#DDDDDD] mt-[10px] ml-[10px]"
        @click="handleDeleteAll"
      >
        Delete All
      </button> -->
      <p v-if="civilServants.length" class="text-right m-[20px]">
        {{ peopleCount }} people in the list
      </p>
      <div class="bg-white shadow-lg rounded-lg">
        <div v-if="civilServants.length < 1" class="pb-[200px] pt-[150px]">
          <svg
            class="svg-icon mx-auto"
            style="
              width: 200px;
              height: 200px;
              vertical-align: middle;
              fill: currentColor;
              overflow: hidden;
            "
            viewBox="0 0 1567 1024"
            version="1.1"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M156.662278 699.758173h21.097186A10.444152 10.444152 0 0 1 187.994733 710.202325c0 5.765172-4.490985 10.444152-10.235269 10.444152H156.662278v21.097186A10.444152 10.444152 0 0 1 146.218126 751.978932a10.277045 10.277045 0 0 1-10.444152-10.235269V720.646477H114.676787A10.444152 10.444152 0 0 1 104.441518 710.202325c0-5.765172 4.490985-10.444152 10.235269-10.444152H135.773974v-21.097187A10.444152 10.444152 0 0 1 146.218126 668.425717c5.765172 0 10.444152 4.490985 10.444152 10.235269v21.097187z m1378.628042-83.553215v-21.097186A10.277045 10.277045 0 0 0 1524.846168 584.872503a10.444152 10.444152 0 0 0-10.444152 10.235269v21.097186h-21.097186a10.277045 10.277045 0 0 0-10.235269 10.444152c0 5.598065 4.595427 10.444152 10.235269 10.444152h21.097186v21.097187c0 5.744284 4.67898 10.235269 10.444152 10.235268a10.444152 10.444152 0 0 0 10.444152-10.235268V637.093262h21.097187c5.744284 0 10.235269-4.67898 10.235268-10.444152a10.444152 10.444152 0 0 0-10.235268-10.444152H1535.29032zM776.460024 960.861969H250.596979A20.80475 20.80475 0 0 1 229.77134 939.973665c0-11.530344 9.462402-20.888304 20.825639-20.888303h94.728457A83.010119 83.010119 0 0 1 334.212859 877.413196v-605.96969A83.49055 83.49055 0 0 1 417.849627 187.994733H480.430984V167.001988A83.49055 83.49055 0 0 1 564.067752 83.553215h501.152182A83.448773 83.448773 0 0 1 1148.856702 167.001988v605.969689c0 15.185797-4.052331 29.410732-11.133466 41.672166h115.554096c11.551232 0 20.909192 9.274407 20.909192 20.888304 0 11.530344-9.295295 20.888304-20.888304 20.888304H1002.638576v20.992745c0 15.185797-4.052331 29.410732-11.133466 41.672166h11.196131c11.488567 0 20.825639 9.274407 20.825639 20.888303 0 11.530344-9.462402 20.888304-20.825639 20.888304h-109.893365c9.545955 16.000441 7.478013 36.972297-6.41271 50.863019a41.672166 41.672166 0 0 1-59.072122 0L776.460024 960.861969z m76.367638-41.776607h66.424806c22.977134 0 41.609501-18.59059 41.609501-41.881049V270.461756c0-22.559368-18.047494-40.690416-40.314426-40.690416H416.303892c-22.266932 0-40.314426 18.214601-40.314426 40.690416v606.742557c0 23.123352 18.799473 41.881049 41.588613 41.881049h317.084449l-10.736588-10.757477a41.693054 41.693054 0 0 1-10.861918-40.377091l-19.718558-19.739447A146.259902 146.259902 0 0 1 502.363703 627.693525a146.218126 146.218126 0 0 1 220.517822 190.981761l19.739447 19.739447a41.630389 41.630389 0 0 1 40.377091 10.841029L852.827662 919.085362zM1002.638576 814.643843h62.852906A41.797496 41.797496 0 0 0 1107.080095 772.867236V167.106429c0-23.14424-18.632367-41.776607-41.588613-41.776607H563.775316A41.797496 41.797496 0 0 0 522.207592 167.106429v20.888304h396.794216A83.448773 83.448773 0 0 1 1002.638576 271.443506V814.643843zM266.325872 46.998683h31.123572c8.773088 0 15.875111 6.955805 15.875111 15.666228 0 8.647758-7.102023 15.666228-15.875111 15.666228h-31.123572v31.123572c0 8.773088-6.955805 15.875111-15.666228 15.875111a15.770669 15.770669 0 0 1-15.666228-15.875111V78.331139H203.869844A15.728893 15.728893 0 0 1 187.994733 62.664911c0-8.647758 7.102023-15.666228 15.875111-15.666228h31.123572V15.875111c0-8.773088 6.955805-15.875111 15.666228-15.875111 8.647758 0 15.666228 7.102023 15.666228 15.875111v31.123572zM20.888304 939.973665c0-11.530344 9.462402-20.888304 20.825638-20.888303h125.455152c11.488567 0 20.825639 9.274407 20.825639 20.888303 0 11.530344-9.462402 20.888304-20.825639 20.888304H41.713942A20.80475 20.80475 0 0 1 20.888304 939.973665z m658.733544-135.021995a104.441518 104.441518 0 1 0-147.722083-147.722083 104.441518 104.441518 0 0 0 147.722083 147.722083zM459.542681 313.324555a20.888304 20.888304 0 0 1 20.867415-20.888304H710.202325a20.888304 20.888304 0 1 1 0 41.776608H480.430984A20.825639 20.825639 0 0 1 459.542681 313.324555z m0 104.441518c0-11.530344 9.295295-20.888304 20.742085-20.888303h334.505295c11.44679 0 20.742086 9.274407 20.742086 20.888303 0 11.530344-9.295295 20.888304-20.742086 20.888304H480.284766A20.762974 20.762974 0 0 1 459.542681 417.766073z m0 104.441519c0-11.530344 9.316183-20.888304 20.846527-20.888304h146.301679c11.509455 0 20.846527 9.274407 20.846527 20.888304 0 11.530344-9.316183 20.888304-20.846527 20.888303h-146.301679A20.80475 20.80475 0 0 1 459.542681 522.207592zM62.664911 396.87777a62.664911 62.664911 0 1 1 0-125.329822 62.664911 62.664911 0 0 1 0 125.329822z m0-31.332456a31.332456 31.332456 0 1 0 0-62.664911 31.332456 31.332456 0 0 0 0 62.664911zM1357.739739 271.547948a62.664911 62.664911 0 1 1 0-125.329822 62.664911 62.664911 0 0 1 0 125.329822z m0-31.332456a31.332456 31.332456 0 1 0 0-62.664911 31.332456 31.332456 0 0 0 0 62.664911z"
              fill="#8A96A3"
            />
          </svg>
          <p
            class="text-[#555555] text-[20px] font-normal leading-[18px] flex justify-center items-center h-full"
          >
            No Data Available!
          </p>
        </div>

        <table
          v-if="civilServants.length"
          class="min-w-full border-collapse border border-[#DDDDDD]"
        >
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
              :class="{
                'border border-[#DDDDDD] hover:bg-gray-50 text-sm font-normal leading-[18px] text-left text-[#000000]': true,
                'cursor-grab': !isSorted,
                'cursor-unset': isSorted,
              }"
              :draggable="!isSorted"
              @dragstart="handleDragStart(index)"
              @dragover="handleDragOver"
              @drop="handleDrop(index)"
              @dragend="handleDragEnd"
            >
              <td class="p-3 flex items-center gap-2 px-[20px]">
                <input
                  type="checkbox"
                  :checked="index === 3 || index === 5"
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
            <tr
              v-if="draggedIndex !== null"
              class="empty-row"
              @dragover="handleDragOver"
              @drop="handleDrop(civilServants.length)"
            >
              <td class="p-[25px] flex items-center gap-2 px-[20px]"></td>
              <td class="p-[25px] border-l border-[#DDDDDD] pl-[40px]"></td>
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
        <h2 class="text-[14px] font-bold leading-[22px]">
          {{
            isSorted
              ? !resultShown
                ? 'Congratulations! Table is sorted properly!'
                : 'Sort Again?'
              : civilServants?.length
              ? 'Table has been generated!'
              : 'How many people?'
          }}
        </h2>

        <svg
          width="12"
          height="12"
          viewBox="0 0 12 12"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
          xmlns:xlink="http://www.w3.org/1999/xlink"
          @click="toggleModal"
          class="cursor-pointer"
          v-if="!civilServants?.length || resultShown"
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
      <div
        v-if="!isSorted && !civilServants?.length"
        class="px-[20px] pt-[20px] h-[150px]"
      >
        <p class="text-[#555555] text-[13px] font-normal leading-[18px]">
          Enter a number of how many people you want to add to the list.
        </p>

        <input
          v-model.number="peopleCount"
          type="number"
          :class="{
            'mt-4 w-full px-3 py-2 border border-[#CCCCCC] rounded-[5px] outline-none': true,
            'border-red-500': peopleCount < 20 || peopleCount > 100,
          }"
          placeholder="Enter a number between 20 and 100"
        />
        <p
          v-if="peopleCount < 20 || peopleCount > 100"
          class="text-red-500 text-sm pt-[6px]"
        >
          Please enter a number between 20 and 100
        </p>
      </div>

      <div
        v-if="(!isSorted && civilServants?.length) || resultShown"
        class="px-[20px] pt-[14px] flex-column justify-center"
      >
        <svg
          width="35px"
          height="35px"
          version="1.1"
          id="Layer_1"
          xmlns="http://www.w3.org/2000/svg"
          xmlns:xlink="http://www.w3.org/1999/xlink"
          viewBox="0 0 495 495"
          xml:space="preserve"
          class="mx-auto block"
        >
          <g>
            <path
              style="fill: #ff3501;"
              d="M267.5,60.915V40h-40v20.915c6.611-0.599,13.281-0.915,20-0.915S260.889,60.316,267.5,60.915z"
            />
            <rect
              x="184.231"
              style="fill: #cd2a00;"
              width="126.537"
              height="40"
            />
            <path
              style="fill: #cd2a00;"
              d="M376.917,73.716l-35.428-18.572l-11.089,21.152c12.32,5.076,24.161,11.309,35.401,18.624
		L376.917,73.716z"
            />
            <path
              style="fill: #cd2a00;"
              d="M153.511,55.144l-35.428,18.572l11.116,21.204c11.24-7.315,23.081-13.548,35.401-18.624
		L153.511,55.144z"
            />
            <path
              style="fill: #e0e0e2;"
              d="M227.5,297.5V150h20v-50C149.626,100,70,179.626,70,277.5S149.626,455,247.5,455V297.5H227.5z"
            />
            <path
              style="fill: #c6c5ca;"
              d="M247.5,100v50h20v107.5H375v40H247.5V455c97.874,0,177.5-79.626,177.5-177.5S345.374,100,247.5,100z
		"
            />
            <path
              style="fill: #ff5023;"
              d="M401.296,123.704c-10.933-10.933-22.833-20.545-35.495-28.785
		c-11.24-7.315-23.081-13.548-35.401-18.624c-19.916-8.205-41.07-13.403-62.901-15.38c-6.611-0.599-13.281-0.915-20-0.915
		s-13.389,0.316-20,0.915c-21.83,1.978-42.985,7.175-62.901,15.38c-12.32,5.076-24.161,11.309-35.401,18.624
		c-12.661,8.24-24.562,17.852-35.495,28.785C52.624,164.784,30,219.403,30,277.5s22.624,112.716,63.704,153.796
		S189.403,495,247.5,495s112.716-22.624,153.796-63.704S465,335.597,465,277.5S442.376,164.784,401.296,123.704z M247.5,455
		C149.626,455,70,375.374,70,277.5S149.626,100,247.5,100S425,179.626,425,277.5S345.374,455,247.5,455z"
            />
            <polygon
              style="fill: #005ece;"
              points="227.5,297.5 375,297.5 375,257.5 267.5,257.5 267.5,150 227.5,150 	"
            />
          </g>
        </svg>
        <p
          class="text-[#555555] text-[14px] font-normal leading-[18px] flex items-center pt-[10px]"
        >
          The faster you sort the table in descending order, the higher your
          score. If you click "Okay" a timer will start and you have to start
          sorting.
        </p>
        <p
          v-if="civilServants?.length"
          class="text-[#555555] text-[14px] font-normal leading-[18px] px-[20px] pb-[14px] text-center"
        >
          Good luck! 🚀
        </p>
      </div>

      <div
        v-if="isSorted && !resultShown"
        class="px-[20px] py-[24px] flex flex-col items-center justify-center border-t border-[#CCCCCC]"
      >
        <p
          class="text-[#555555] text-[14px] font-normal leading-[20px] flex items-center pt-[10px]"
        >
          ✅ Time Taken: {{ Math.floor((timer % 3600) / 60) }} min
          {{ timer % 60 }} sec
          <br />
          👥 People Sorted: {{ peopleCount }}
          <br />
          ⭐ Final Score: {{ finalScore.toFixed(2) }}
        </p>
        <p
          class="text-[#555555] text-[14px] font-normal leading-[18px] flex items-center pt-[4px]"
          v-if="finalScore >= 100"
        >
          🔥Ranking Badge: Sorting Master (Score ≥ 100)
        </p>
        <p
          class="text-[#555555] text-[14px] font-normal leading-[18px] flex items-center pt-[4px]"
          v-else-if="finalScore >= 70"
        >
          ⚡Ranking Badge: Pro Sorter (Score 70 – 99)
        </p>
        <p
          class="text-[#555555] text-[14px] font-normal leading-[18px] flex items-center pt-[4px]"
          v-else-if="finalScore >= 40"
        >
          ⏳Ranking Badge: Skilled Sorter (Score 40 – 69)
        </p>
        <p
          class="text-[#555555] text-[14px] font-normal leading-[18px] flex items-center pt-[4px]"
          v-else
        >
          🐢Ranking Badge: Keep Practicing (Score < 40)
        </p>
      </div>
      <div
        :class="
          'flex space-x-2 py-[20px] px-[20px] border-t border-[#CCCCCC] ' +
          (!civilServants?.length ? 'justify-end' : 'justify-center')
        "
      >
        <button
          v-if="!civilServants?.length"
          @click="toggleModal"
          class="px-4 py-2 text-[#555555] rounded-md border border-transparent hover:border-[#555555] text-[14px] font-bold leading-[16.41px] bg-gray-100 cursor-pointer"
        >
          Cancel
        </button>
        <button
          @click="handleStart"
          class="px-4 py-2 bg-orange-500 text-white rounded-md hover:bg-orange-600 disabled:opacity-50 text-[14px] font-bold leading-[16.41px] cursor-pointer"
          :disabled="peopleCount < 20 || peopleCount > 100"
        >
          {{ civilServants?.length ? 'Okay' : 'Start' }}
        </button>
      </div>
    </div>
  </div>
</template>
