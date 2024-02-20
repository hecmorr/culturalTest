<script setup lang="ts">
import imgUrl from '../images/HL-LOGO-WHITE FONTRGB_HORIZONTAL-INV.png'
import { ref } from 'vue'

const name = ref('')
const position = ref('')
const email = ref('')
const scriptUrl =
  'https://script.google.com/macros/s/AKfycbwLeps_uHAdmFUQOlQhxHR9MgCbFHwm7PuuNRcWPCbTp71nVYJw4_MqP2QYvCMaXPv4/exec'

const selectedCategories = ref<string[]>([])
const categories = {
  commander: {
    structured: 'Structured',
    organized: 'Organized',
    hierarchical: 'Hierarchical',
    efficient: 'Efficient',
    traditional: 'Traditional',
    ruleFollowing: 'Rule-Following',
    disciplined: 'Disciplined',
    formal: 'Formal',
    authoratative: 'Authoritative',
    procedureOriented: 'Procedure-Oriented',
    systematic: 'Systematic',
    methodical: 'Methodical',
    orderly: 'Orderly',
    predictable: 'Predictable',
    stability: 'Stability'
  },
  venturer: {
    dynamicVenturer: 'Dynamic-Venturer',
    riskTaking: 'Risk-Taking',
    innoveative: 'Innovative',
    agile: 'Agile',
    unconventional: 'Unconventional',
    creative: 'Creative',
    experimental: 'Experimental',
    opportunistic: 'Opportunistic',
    pioneer: 'Pioneer',
    visionary: 'Visionary',
    explorative: 'Explorative',
    changeEmbracing: 'Change-Embracing',
    resourceful: 'Resourceful'
  },
  hustler: {
    competitive: 'Competitive',
    goalOriented: 'Goal-Oriented',
    pragmatic: 'Pragmatical',
    ambitious: 'Ambitious',
    markFocused: 'Mark-Focused',
    resultDrive: 'Result-Driven',
    assertive: 'Assertive',
    driven: 'Driven',
    achievementFocused: 'Achievement-Focused',
    leader: 'Leader',
    proactive: 'Proactive',
    persistent: 'Persistent',
    resilient: 'Resilient',
    dynamic: 'Dynamic'
  },
  teamplayer: {
    collaborative: 'Collaborative',
    inclusive: 'Inclusive',
    communityMinded: 'Community-minded',
    trusting: 'Trusting',
    supportive: 'Supportive',
    teamFocused: 'Team-focused',
    empathetic: 'Empathetic',
    harmonious: 'Harmonious',
    cooperative: 'Cooperative',
    consensusSeeking: 'Consensus-seeking',
    pioneeringCommunicator: 'Pioneering Communicator',
    relationshipOriented: 'Relationship-oriented',
    interpersonal: 'Interpersonal',
    groupCentric: 'Group Centric',
    participative: 'Participative'
  },
  adapter: {
    versatile: 'Versatile',
    openMinded: 'Open-minded',
    integrative: 'Integrative',
    flexible: 'Flexible',
    learningOriented: 'Learning-oriented',
    multifaceted: 'Multifaceted',
    adaptable: 'Adaptable',
    diverse: 'Diverse',
    eclectic: 'Eclectic',
    tolerant: 'Tolerant',
    curious: 'Curious',
    broadMinded: 'Broad-minded',
    absorptive: 'Absorptive',
    responsive: 'Responsive',
    elastic: 'Elastic'
  }
}

const cleanInput = async () => {
  name.value = ''
  email.value = ''
  position.value = ''
  selectedCategories.value = []
}

const checkResult = async () => {
  const attributesTotal = {
    commander: 0,
    venturer: 0,
    hustler: 0,
    teamplayer: 0,
    adapter: 0
  }
  for (const key in categories) {
    let total = 0
    if (Object.prototype.hasOwnProperty.call(categories, key)) {
      Object.values(categories[key as keyof typeof categories]).forEach((attribute) => {
        if (selectedCategories.value.some((value) => value == attribute)) {
          total += 1
        }
      })
      attributesTotal[key as keyof typeof attributesTotal] = total
    }
  }
  const maxKey = Object.keys(attributesTotal).reduce((a, b) =>
    attributesTotal[a as keyof typeof attributesTotal] >
    attributesTotal[b as keyof typeof attributesTotal]
      ? a
      : b
  )

  const formData = new FormData()
  formData.append('name', `${name.value}`)
  formData.append('email', `${email.value}`)
  formData.append('position', `${position.value}`)
  formData.append('result', `${maxKey}`)

  try {
    await submit(formData)
    window.alert(`Hello ${name.value}, your form has been succesfully submitted`)
    cleanInput()
  } catch (error) {
    return error
  }
}

const validateForm = () => {
  if (name.value.length < 1) {
    alert('Please enter your name')
    throw Error('Name is required')
  } else if (email.value.length < 1) {
    alert('Please enter your email')
    throw Error('Email is required')
  } else if (position.value.length < 1) {
    alert('Please enter the position you are applying to')
    throw Error('Position is required')
  }
}

const submit = async (formData: FormData) => {
  validateForm()
  const response = await fetch(scriptUrl, {
    body: formData,
    method: 'POST',
    mode: 'no-cors'
  }).catch((error) => console.log(`Error!: ${error.message}`))
}
</script>

<template>
  <header
    class="flex flex-col content-center place-items-center gap-2 w-full h-[250px] lg:flex-row lg:h-[150px] lg:justify-evenly py-2 bg-purple-400 shadow-md"
  >
    <img :src="imgUrl" alt="HireLatam logo" class="w-[250px] h-24" />
    <h3 class="lg:w-28 font-extrabold">Cultural Test</h3>
    <form
      id="form"
      class="flex flex-col gap-y-2 w-full place-items-center lg:gap-x-2 lg:w-auto content-center lg:flex-row"
    >
      <div class="flex w-4/5 lg:w-[280px] lg:gap-x-2">
        <label for="name" class="w-28 lg:w-fit">Name: </label>
        <input
          class="border rounded-md w-40 shadow-md"
          type="text"
          name="name"
          v-model="name"
          required
        />
      </div>
      <div class="flex w-4/5 lg:w-[280px] lg:gap-x-2">
        <label for="email" class="w-28 lg:w-fit">Email: </label>
        <input
          class="border rounded-md w-40 shadow-md"
          type="text"
          name="email"
          v-model="email"
          required
        />
      </div>
      <div class="flex w-4/5 lg:w-[280px] lg:gap-x-2">
        <label for="position" class="w-28 lg:w-fit">Job position: </label>
        <input
          class="border rounded-md w-40 shadow-md"
          type="text"
          name="position"
          v-model="position"
          required
        />
      </div>
    </form>
  </header>
  <main class="flex justify-center">
    <div
      class="flex flex-col gap-4 w-full lg:w-[1000px] h-full lg:h-[1400px] rounded-md border my-5 py-5 shadow-lg"
    >
      <p class="flex text-center lg:justify-center font-extrabold">
        Check the box of those that apply to your personality
      </p>
      <layout-columns class="columns-2 lg:columns-3 justify-center">
        <ul
          class="flex flex-col gap-3 m-2 mx-5 lg:mx-16"
          v-for="(category, index) in Object.values(categories)"
          :key="index"
        >
          <li
            class="flex items-center gap-2 m-2"
            v-for="(attribute, index) in Object.values(category)"
            :key="index"
          >
            <label :for="attribute" class="ms-2 text-sm font-medium text-gray-900">
              {{ attribute }}</label
            >
            <input
              :value="attribute"
              v-model="selectedCategories"
              :id="attribute"
              type="checkbox"
              class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded-full focus:ring-blue-500"
            />
          </li>
        </ul>
      </layout-columns>
      <button
        class="border m-2 font-extrabold rounded-md bg-purple-400 mx-auto h-12 w-40 shadow-md"
        type="submit"
        @click="checkResult"
      >
        Submit
      </button>
    </div>
  </main>
</template>
