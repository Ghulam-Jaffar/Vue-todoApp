<template>
  <div class="flex flex-col justify-center items-center mt-10">
    <p class='font-bold'>My todo App</p>
    {{ msg }}
    <div class="flex mt-2 mx-1">
      <input type="text" placeholder="enter new task" v-model="newTask"
        class="class='form-control block w-11/12 px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-gray-400 rounded transition ease-in-out duration-500 focus:text-gray-700 focus:bg-white focus:border-sky-400 focus:outline-none">
      <button class="rounded w-fit ml-1 p-2 border-2 border-sky-300" @click="addTask">ADD</button>
    </div>
    <div v-if="tasks.length < 1">
      <p class="font-bold mt-4 mx-2">Nothing yet to show! Why don't you add some todos :D</p>
    </div>
    <div v-else
      class=" mt-5 rounded-sm flex flex-1 justify-center items-center sm:w-full md:w-10/12 lg:w-8/12 xl:w-7/12 ">
      <table class="table-auto  border-2 md:w-6/12">
        <thead class="bg-gray-50 border-b-2">
          <tr class="border-2">
            <th class="w-10">#</th>
            <th class="w-full">Task</th>
            <th class='w-20 p-1'>Status</th>
            <th class="w-20 p-1 ">Edit</th>
            <th class="w-20 p-1">Delete</th>
          </tr>
        </thead>
        <tbody class='bg-slate-200 overflow-auto'>

          <tr v-for="(task, index) in tasks" :key="index" class="m-10 border-y-4 border-slate-100 ">
            <td class="text-center w-10">{{ index + 1 + '.' }}</td>
            <td class="text-center w-full cursor-pointer" :class="{ completion: task.completion }"
              @click="toggleTask(index)">{{
                  task.name
              }}</td>

            <td class="text-center cursor-pointer w-20" @click="toggleTask(index)"
              :class="{ statusGreen: task.completion, statusRed: !task.completion }">{{
                  task.completion ? "Finished" : "To-do"
              }}</td>
            <td class="w-20">

              <svg xmlns="http://www.w3.org/2000/svg" class='h-5 w-full text-green-600 cursor-pointer'
                viewBox="0 0 20 20" fill="currentColor" @click="editTask(index)">
                <path d="M17.414 2.586a2 2 0 00-2.828 0L7 10.172V13h2.828l7.586-7.586a2 2 0 000-2.828z" />
                <path fillRule="evenodd"
                  d="M2 6a2 2 0 012-2h4a1 1 0 010 2H4v10h10v-4a1 1 0 112 0v4a2 2 0 01-2 2H4a2 2 0 01-2-2V6z"
                  clipRule="evenodd" />
              </svg>

            </td>
            <td class='w-20'>

              <svg xmlns="http://www.w3.org/2000/svg" class='h-5 w-full text-red-600 cursor-pointer' viewBox="0 0 20 20"
                fill="currentColor" @click="deleteTask(index)">
                <path fillRule="evenodd"
                  d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z"
                  clipRule="evenodd" />
              </svg>

            </td>
            <!-- <td class="text-center ">858</td> -->
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TodoApp',
  props: {
    msg: String,
  },
  data() {
    return {
      tasks: [

      ],
      newTask: null,
      editedTask: null,
    }
  },

  methods: {
    addTask() {
      if (this.newTask && this.editedTask === null) {
        this.tasks.push({ name: this.newTask, completion: false })
        this.newTask = null
      } else {
        this.tasks[this.editedTask].name = this.newTask
        this.editedTask = null
        this.newTask = null
      }
    },
    editTask(index) {
      this.newTask = this.tasks[index].name
      this.editedTask = index
    },
    deleteTask(index) {
      this.tasks.splice(index, 1)
    }, toggleTask(index) {
      this.tasks[index].completion = !this.tasks[index].completion
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.completion {
  text-decoration: line-through;
}

.statusGreen {
  color: green;
}

.statusRed {
  color: red;
}
</style>
