<script setup>
import { ref } from 'vue'


defineProps({
  msg: String,
})


const count = ref(0)
 
</script>
<style scoped>
.read-the-docs {
  color: #888;
}


</style>

<template>
  <div>
    <label for="title" class="block text-sm font-medium text-gray-700">Film Title</label>
    <div class="mt-1">
    <input @change.prevent="write"  v-model="title" type="text" name="title" id="title" class="shadow-sm focus:ring-red-500 focus:border-red-500 block w-full sm:text-sm border-gray-300 rounded-md" placeholder="ex Hamlet ..." aria-describedby="email-description" />
    </div>
    <p class="mt-2 text-sm text-gray-500" id="title-description">Well show film details by title. {{title}}</p>
  <button @click.prevent="send"  type="button" :class="isDisabled">
  Send
  </button>

  </div>
  <div v-if="loading" id="loading" class="flex items-center justify-center mt-15">
    <div class="flex space-x-2 animate-pulse">
        <div class="w-3 h-3 bg-red-500 rounded-full"></div>
        <div class="w-3 h-3 bg-red-500 rounded-full"></div>
        <div class="w-3 h-3 bg-red-500 rounded-full"></div>
    </div>
  </div>
  <div v-if="isReady" id="result">
    <div class="flex flex-col">
    <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
      <div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
        <div class="shadow overflow-hidden border-b border-gray-200 sm:rounded-lg">
          <table class="min-w-full divide-y divide-gray-200">
            <thead class="bg-gray-50">
              <tr>
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  Title
                </th>
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  IsAdulte
                </th>
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  duration
                </th>
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  crew
                </th>
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  cast
                </th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(person, personIdx) in people" :key="person.email" :class="personIdx % 2 === 0 ? 'bg-white' : 'bg-gray-50'">
                <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">
                  {{ person.name }}
                </td>
                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                  {{ person.title }}
                </td>
                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                  {{ person.email }}
                </td>
                <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                  {{ person.role }}
                </td>
                <td class="px-6 py-4 whitespace-nowrap text-right text-sm font-medium">
                  <a href="#" class="text-red-600 hover:text-red-900">Edit</a>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</div>

</template>
<script>
import {ref} from 'vue'
import axios from 'axios'
const backendLink = "http://ec2-3-90-50-56.compute-1.amazonaws.com:8080"
 const people = [
  { name: 'Jane Cooper', title: 'Regional Paradigm Technician', role: 'Admin', email: 'jane.cooper@example.com' },
  { name: 'Cody Fisher', title: 'Product Directives Officer', role: 'Owner', email: 'cody.fisher@example.com' },
  // More people...
]
const title = ref('')
export default {
  setup() {

    const loading = ref(false)
    const isReady = ref(false)
    let disabled = ref(true)
  return {
      people,
      loading,
      isReady,
      disabled,
      title
    }
  },
  methods: {
    write() {
       this.disabled = false
    console.log(title)
    this.$forceUpdate()
    },
  send(){
    const url = backendLink+ '/films/'+title.value;
  axios.defaults.headers.common['Access-Control-Allow-Origin'] = '*';


     if(title.value !== ''){
     fetch(url, {
     "method": "GET",
     "headers": {
     "Content-Type": "application/json",
     "Access-Control-Allow-Origin": "*"
     }
     })
     .then(response => {
console.log(response);
})
     .catch(err => {
console.error(err);
});
     }
  }
  },
  computed : {
    isDisabled(){
    return {
    'inline-flex items-center px-3 py-2 border border-transparent text-sm leading-4 font-medium rounded-md shadow-sm text-white bg-red-600 hover:bg-red-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-red-500': title.value !== '' ,
    'inline-flex items-center px-3 py-2 border border-transparent text-sm leading-4 font-medium rounded-md shadow-sm text-white bg-grey-600 hover:bg-grey-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-grey-500' : title.value === ''
  }
    },
updated() {
console.log("updated")
}
}
        }
</script>



