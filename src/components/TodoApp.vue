to do app vue js

<template>
    <div class="container">
        <h1 class="text-center"> Todo App</h1>
        <div>
        <input type="text" v-model="task" placeholder="" />
        <select v-model="priority" class="priority-select">
            <option value="low">Low</option>
            <option value="medium">Medium</option>
            <option value="high">High</option>
        </select>
        <button class="add-btn" @click="submitTask">ADD</button>
    </div>

    <div>
        <button @click="showActive = true">Active</button>
        <button @click="showActive = false">Done</button>
    </div>

    <!-- Summary section -->
    <div class="summary">
        <div class="summary-box">
            <h3>Pending Tasks: {{ pendingTasks }}</h3>
        </div>
        <div class="summary-box">
            <h3>Low Priority: {{ lowPriorityTasks }}</h3>
        </div>
        <div class="summary-box">
            <h3>Medium Priority: {{ mediumPriorityTasks }}</h3>
        </div>
        <div class="summary-box">
            <h3>High Priority: {{ highPriorityTasks }}</h3>
        </div>
        </div>

    <!-- Table section -->
    <table border="3">
        <thead>
            <tr v-if="showActive">
                <th>ID</th>
                <th>Task</th>
                <th>Priority</th>
                <th>Delete</th>
                <th>Done</th>
            </tr>
            <tr v-else>
                <th>ID</th>
                <th>Task</th>
                <th>Priority</th>
                <th>Delete</th>
            </tr>
        </thead>
        <tbody>
            <template v-for="(task, index) in filteredTasks" :key="index">
                <tr>
                    <td>{{ task.id }}</td>
                    <td>{{ task.name }}</td>
                    <td>{{ task.priority }}</td>
                        <td v-if="showActive">
                            <button class="del-btn" @click="deleteTask(index)">Delete</button>
                        </td>
                    <td v-else>
                        <button class="done-btn" @click="toggleDone(index)">
                            {{ task.done ? 'Undo' : 'Done' }}
                        </button>
                    </td>
                </tr>
            </template>
        </tbody>
    </table>
    </div>
</template>

<script>
    export default {
    name: "TodoApp",
    data() {
        return {
        task: "",
        priority: "low",
        editTask: null,
        tasks: [
            {
                name: "Kerja Tugas 1",
                id: Date.now() + 1,
                done: false,
                priority: "medium",
        },
            {
                name: "Belajar Vue js",
                id: Date.now() + 2,
                done: false,
                priority: "low",
        },
            {
                name: "Error dan Debugging",
                id: Date.now() + 3,
                done: false,
                priority: "high",
        },
        ],
        showActive: true,
    };
},
    computed: {
        pendingTasks() {
            return this.tasks.filter((task) => !task.done).length;
        },
        lowPriorityTasks() {
            return this.tasks.filter((task) => task.priority === "low").length;
        },
        mediumPriorityTasks() {
            return this.tasks.filter((task) => task.priority === "medium").length;
        },
        highPriorityTasks() {
            return this.tasks.filter((task) => task.priority === "high").length;
        },
        filteredTasks() {
            return this.showActive
                ? this.tasks.filter((task) => !task.done)
                : this.tasks.filter((task) => task.done);
        },
    },
    methods: {
        toggleDone(index) {
            this.tasks[index].done = !this.tasks[index].done;
        },
        deleteTask(index) {
            this.tasks.splice(index, 1);
        },
        submitTask() {
            if (this.task.length === 0) {
            return;
        }
            if (this.editTask !== null && this.editTask !== undefined) {
                this.tasks[this.editTask].name = this.task;
                this.tasks[this.editTask].priority = this.priority;
                this.editTask = null;
            } else {
                this.tasks.push({
                name: this.task,
                id: Date.now() + 4,
                done: false,
                priority: this.priority,
            });
        }
            this.task = "";
            this.priority = "low";
        },
    },
};
</script>

<style scoped>
    .container {
        width: 600px;
        margin: auto;
    }

    table {
        font-family: arial, sans-serif;
        border-collapse: collapse;
        width: 100%;
        margin-top: 20px;
    }

    td,
    th {
        border: 1px solid #dddddd;
        text-align: center;
        padding: 8px;
    }

    tr:nth-child(even) {
        background-color: #dddddd;
}
    .add-btn {
        border: none;
        width: 100px;
        height: 30px;
        padding: 2px;
        background-color: teal;
        color: white;
    }

    .del-btn {
        border: none;
        background-color: red;
        color: white;
    }

    .done-btn {
        border: none;
        background-color: #77b631;
        color: white;
    } 
    .priority-select {
        margin-left: 10px;
    }
    .summary {
        display: flex;
        justify-content: space-around;
        margin-bottom: 20px;
    }
    .summary-box {
        border: 1px solid #ddd;
        padding: 10px;
        text-align: center;
        flex: 1;
        margin: 0 5px;
}
</style>

