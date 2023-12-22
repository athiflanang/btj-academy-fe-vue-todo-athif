sparsing error
<template v-for="(task, index) in filteredTasks" :key="index">
      <tr>
            <td>{{ task.id }}</td>
            <td>{{ task.name }}</td>
            <td>{{ task.priority }}</td>
                <td v-if="showActive">
                    <button class="del-btn" @click="deleteTask(index)">Delete</button>
                </td>
            <td v-else>
                <td>
                    <button class="done-btn" @click="toggleDone(index)">
                          {{ task.done ? 'Undo' : 'Done' }}
                    </button>
                </td>
            </td> <---- error sparsing
      </tr>
</template>
           
