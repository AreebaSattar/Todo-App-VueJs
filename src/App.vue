<template>

  <div class="w-full mx-w-2xl mx-3 ">
    <div class="text-center mb-5">
      <h1 class="text-4xl uppercase font-bold">TODO App</h1>
    </div>
    <div>
      <form class="flex justify-center" @submit.prevent="addTasks()" action="#" method="post">
        <select class="rounded-l-full bg-emerald-100 px-3 py-1 placeholder-emerald-600 text-emerald-600"
                v-model="selectedCategory">
          <option value="">Select Category</option>
          <option v-for="category in categories" :key="category" :value="category"> {{ category }}</option>
        </select>
        <input class=" bg-emerald-100 px-3 py-1 placeholder-emerald-600" type="text" placeholder="Add To-do"
               v-model="newTask"/>
        <date-picker v-model:value="selectedDate" type="datetime" placeholder="Select datetime"></date-picker>
        <button class="rounded-r-full text-white bg-emerald-500 px-3 py-1" type="submit" value="+">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
               stroke="currentColor" class="size-6">
            <path stroke-linecap="round" stroke-linejoin="round" d="M12 4.5v15m7.5-7.5h-15"/>
          </svg>
        </button>
      </form>
    </div>
    <div class="bg-white mt-1 p-4 rounded-3xl shadow-xl">
      <div>
        <h1 class="text-lg font-bold mb-0 leading-none">Todos </h1>
        <small class="text-xs inline-block mt-0 text-gray-700">{{ remainingTasks }} todos pending, {{ completedTasks }}
          completed</small>
      </div>
      <div class="mt-2 overflow-y-auto max-h-60">
        <table class="w-full">
          <thead>
          <tr class="bg-emerald-600 text-emerald-100">
            <th class="text-center p-2 rounded-tl-lg">#</th>
            <th class="text-left p-2 w-full">Details</th>
            <th class="text-left p-2 w-full">Category</th>
            <th class="text-left p-2 w-full ">Start Time</th>
            <th class="text-left p-2 rounded-tr-lg">Actions</th>
          </tr>
          </thead>
          <tbody>
          <tr v-if="tasks.length === 0" class="bg-emerald-100">
            <td colspan="5" class="p-2 rounded-b-lg">
              No Tasks to do. You can add them from above form.
            </td>
          </tr>
          <tr v-for="(task,index) in tasks" :key="index"
              :class="`text-emerald-700 ${!task.completed ? 'odd:bg-emerald-100 even:bg-emerald-50' : 'bg-cyan-400 line-through'}`">
            <td class="p-2 text-center">{{ index + 1 }}</td>
            <td class="p-2 text-left">{{ task.text }}</td>
            <td class="p-2 text-left">{{ task.category }}</td>
            <td class="p-2 text-left">{{ formatDate(task.startTime) }}</td>
            <td class="p-2 text-left flex gap-3">
              <button @click.prevent="completedTask(index)" v-if="!task.completed">
                <svg height="24" viewBox="0 0 520 520" width="24" xmlns="http://www.w3.org/2000/svg">
                  <g id="_7-Check" data-name="7-Check">
                    <path
                        d="m199.078 473.954a41.224 41.224 0 0 1 -32.441-15.5l-113.88-139.504a45.67 45.67 0 0 1 33.929-74.529c.489-.015.981-.023 1.471-.023a45.552 45.552 0 0 1 30.717 11.892l77.239 70.288a12 12 0 0 0 8.076 3.125q.324 0 .648-.018a12 12 0 0 0 8.339-4.029l236.835-267.589q.156-.177.306-.36a13.234 13.234 0 0 1 9.441-4.839c.318-.021.646-.033.973-.033a13.222 13.222 0 0 1 9.125 3.592c4.524 4.189 6 11.326 3.227 15.586-.047.072-236.657 381.132-236.657 381.132-8.138 12.428-20.89 19.988-35 20.746-.782.042-1.57.063-2.344.063z"
                        fill="#b0ef8f"/>
                    <path
                        d="m460.734 64.835a1.245 1.245 0 0 1 .969.4 2.69 2.69 0 0 1 .705 1.218l-236.1 380.234c-6.109 9.264-15.169 14.668-25.532 15.224-.568.031-1.141.046-1.705.046a29.43 29.43 0 0 1 -23.143-11.09l-113.88-139.5a33.671 33.671 0 0 1 25.012-54.952q.549-.017 1.1-.017a33.575 33.575 0 0 1 22.642 8.768l77.239 70.287a24 24 0 0 0 16.152 6.25c.431 0 .864-.012 1.3-.035a24.005 24.005 0 0 0 16.677-8.059l236.83-267.589q.314-.354.613-.72a1.169 1.169 0 0 1 .954-.459c.057 0 .114-.006.17-.006m0-24c-.6 0-1.2.02-1.8.062a25.176 25.176 0 0 0 -17.9 9.217l-236.847 267.586-77.239-70.288a57.38 57.38 0 0 0 -38.795-15.012q-.923 0-1.85.029a57.67 57.67 0 0 0 -42.845 94.111l113.881 139.5a53.451 53.451 0 0 0 41.736 19.913q1.486 0 2.987-.08c18.021-.968 34.224-10.531 44.484-26.284l236.589-381.027c5.968-9.161 3.715-22.751-5.129-30.94a25.231 25.231 0 0 0 -17.279-6.787z"
                        fill="#009045"/>
                  </g>
                </svg>
              </button>
              <button @click.prevent="NotCompleted(index)" v-if="task.completed">
                <svg height="24" width="24" clip-rule="evenodd" fill-rule="evenodd" image-rendering="optimizeQuality"
                     shape-rendering="geometricPrecision" text-rendering="geometricPrecision" viewBox="0 0 2.54 2.54"
                     xmlns="http://www.w3.org/2000/svg">
                  <g id="&#x56FE;&#x5C42;_x0020_1">
                    <path
                        d="m.37253 0h1.79494c.20518 0 .37253.16735.37253.37253v1.79494c0 .20518-.16735.37253-.37253.37253h-1.79494c-.20518 0-.37253-.16735-.37253-.37253v-1.79494c0-.20518.16735-.37253.37253-.37253z"
                        fill="#ff4141"/>
                    <g id="_411021872" fill="#fff">
                      <path id="_411027656"
                            d="m.6281 1.72969 1.10159-1.10159c.02638-.02637.06941-.02637.09578 0l.08643.08643c.02637.02637.02637.0694 0 .09578l-1.10159 1.10159c-.02638.02637-.06941.02637-.09578 0l-.08643-.08643c-.02637-.02637-.02637-.0694 0-.09578z"/>
                      <path id="_493069600"
                            d="m1.72969 1.9119-1.10159-1.10159c-.02637-.02638-.02637-.06941 0-.09578l.08643-.08643c.02637-.02637.0694-.02637.09578 0l1.10159 1.10159c.02637.02638.02637.06941 0 .09578l-.08643.08643c-.02637.02637-.0694.02637-.09578 0z"/>
                    </g>
                  </g>
                </svg>
              </button>
              <button @click.prevent="removeTask(index)">
                <svg id="Layer_1" height="24" viewBox="0 0 512 512" width="24" xmlns="http://www.w3.org/2000/svg"
                     data-name="Layer 1">
                  <g fill-rule="evenodd">
                    <path
                        d="m443.3 0h-374.6a68.781 68.781 0 0 0 -68.7 68.7v374.6a68.779 68.779 0 0 0 68.7 68.7h374.6a68.778 68.778 0 0 0 68.7-68.7v-374.6a68.781 68.781 0 0 0 -68.7-68.7z"
                        fill="#ff3f5b"/>
                    <path
                        d="m359.45 168.73h-51v-12.86a36.913 36.913 0 0 0 -36.871-36.87h-31.158a36.913 36.913 0 0 0 -36.872 36.87v12.86h-51a12 12 0 0 0 0 24h6.44v168.38a31.932 31.932 0 0 0 31.89 31.89h130.241a31.93 31.93 0 0 0 31.889-31.89v-168.38h6.439a12 12 0 0 0 0-24zm-131.9-12.86a12.878 12.878 0 0 1 12.869-12.87h31.162a12.879 12.879 0 0 1 12.868 12.87v12.86h-56.9v-12.86zm101.46 205.24a8 8 0 0 1 -7.891 7.89h-130.238a8 8 0 0 1 -7.892-7.89v-168.38h146.021zm-111.87-28.02v-100.8a12 12 0 1 1 24 0v100.8a12 12 0 0 1 -24 0zm53.721 0v-100.8a12 12 0 1 1 24 0v100.8a12 12 0 1 1 -24 0z"
                        fill="#fff"/>
                  </g>
                </svg>
              </button>
            </td>
          </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script setup>
import DatePicker from 'vue-datepicker-next';
import 'vue-datepicker-next/index.css';
import {computed, ref} from "vue";

const newTask = ref('');
const selectedCategory = ref('');
const categories = ref(
    [
      'work', 'home', 'family', 'university', 'important',
    ]
);
const selectedDate = ref('');
const tasks = ref([
  {text: 'Learn Vue', completed: false}
]);
const remainingTasks = computed(() => {
  return tasks.value.filter(task => !task.completed).length;
});
const completedTasks = computed(() => {
  return tasks.value.filter(task => task.completed).length;
})
const formatDate = (date) => {
  if (!date) return '';
  return new Date(date).toLocaleDateString('en-US', {
    month: 'short',
    day: 'numeric',
    hour: 'numeric',
    minute: 'numeric',
    second: 'numeric',
  });

}
const addTasks = () => {
  if (newTask.value && selectedCategory.value && selectedDate.value) {
    tasks.value.push({
      text: newTask.value,
      category: selectedCategory.value,
      completed: false,
      startTime: selectedDate.value
    })
    newTask.value = '';
    selectedCategory.value = '';
    selectedDate.value = null;
  } else {
    alert("Kindly fill all the fields.")
  }
}
const completedTask = (index) => {
  tasks.value[index].completed = true;
}
const stack =()=>
{
  const value=0;
}
const NotCompleted = (index) => {
  tasks.value[index].completed = false;
}
const removeTask = (index) => {
  tasks.value.splice(index, 1);
}
</script>
