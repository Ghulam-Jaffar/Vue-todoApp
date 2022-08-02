<template>
  <div class="flex flex-col justify-center items-center mt-10">
    <p class='font-bold'>My todo App</p>
    {{ msg }}
    <div class="flex mt-2">
      <input type="text" placeholder="enter new task" v-model="newTask"
        class="class='form-control block w-11/12 px-3 py-1.5 text-base font-normal text-gray-700 bg-white bg-clip-padding border border-solid border-sky-300 rounded transition ease-in-out duration-500 focus:text-gray-700 focus:bg-white focus:border-sky-600 focus:outline-none">
      <button class="rounded w-fit ml-1 p-2 border-2 border-sky-300" @click="addTask">ADD</button>
    </div>
    <div class="w-8/12 mt-5  rounded-sm shadow-sm">
      <table class="table-auto w-full border-2">
        <thead class="bg-gray-50 border-b-2">
          <tr class="border-2">
            <th class="w-10">#</th>
            <th>Task</th>
            <th class='w-20'>Status</th>
            <th class="w-20">Edit</th>
            <th class="w-20">Delete</th>
          </tr>
        </thead>
        <tbody>

          <tr v-for="(task, index) in tasks" :key="index">
            <td class="text-center">{{ index + 1 }}</td>
            <td class="text-center" :class="{ completion: task.completion}">{{ task.name }}</td>
            <td class="text-center cursor-pointer " @click="toggleTask(index)" :class="{ statusGreen:task.completion, statusRed : !task.completion}" >{{ task.completion }}</td>
            <td>

              <svg xmlns="http://www.w3.org/2000/svg" class='h-5 w-full text-green-600 cursor-pointer'
                viewBox="0 0 20 20" fill="currentColor" @click="editTask(index)">
                <path d="M17.414 2.586a2 2 0 00-2.828 0L7 10.172V13h2.828l7.586-7.586a2 2 0 000-2.828z" />
                <path fillRule="evenodd"
                  d="M2 6a2 2 0 012-2h4a1 1 0 010 2H4v10h10v-4a1 1 0 112 0v4a2 2 0 01-2 2H4a2 2 0 01-2-2V6z"
                  clipRule="evenodd" />
              </svg>

            </td>
            <td>

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
        { name: 'task1', completion: false }, { name: 'task2', completion: false }
      ],
      newTask: null,
      editedTask: null,
    }
  },

  methods: {
    addTask() {
      if (this.newTask && this.editedTask === null) {
        this.tasks.push({ name: this.newTask, completion: false })
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
.completion{
  text-decoration: line-through;
}
.statusGreen{
  color: green;
}
.statusRed{
  color: red;
}
</style>
