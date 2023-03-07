<template>
    <div class="container">
        <div class="box">
            <div class="header">
                <Header text="Task Tracker" />
                <Button text="Add Task" color="white" />
            </div>
            <div v-show="showAddTask">
                <AddTask @add-task="addTask" />
            </div>
            <div class="contents">
                <Tasks
                    @toggleReminder="toggleReminder"
                    @deleteTask="deleteTask"
                    :tasks="tasks" />
            </div>
        </div>
    </div>
</template>

<script>
import Header from "./components/Header.vue";
import Button from "./components/Button.vue";
import Tasks from "./components/Tasks.vue";
import AddTask from "./components/AddTask.vue";

export default {
    name: "App",
    components: {
        Header,
        Button,
        Tasks,
        AddTask,
    },
    data() {
        return {
            tasks: [],
            showAddTask: false,
        };
    },
    created() {
        this.tasks = [
            {
                id: 1,
                text: "Doctors Appointment",
                day: "March 1st at 2:30pm",
                reminder: true,
            },
            {
                id: 2,
                text: "Meeting at School",
                day: "March 3rd at 1:30pm",
                reminder: false,
            },
            {
                id: 3,
                text: "Food Shopping",
                day: "March 4th at 11:30pm",
                reminder: true,
            },
            {
                id: 4,
                text: "Coding Exceptionals",
                day: "March 7th at 8:30pm",
                reminder: false,
            },
        ];
    },
    methods: {
        addTask(task) {
            this.tasks = [...this.tasks, task];
        },
        deleteTask(id) {
            this.tasks = this.tasks.filter((task) => task.id !== id);
        },
        toggleReminder(id) {
            this.tasks = this.tasks.map((task) =>
                task.id == id ? { ...task, reminder: !task.reminder } : task
            );
        },
    },
};
</script>

<style scope>
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@100;200;300;400;500&family=Poppins:wght@100;200;300;400&display=swap");

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: "Montserrat", sans-serif;
}

*::selection {
    background-color: transparent;
}

body {
    width: 100vw;
    height: 100vh;
    background-color: black;
}

.container {
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: flex-start;
}

.box {
    width: 370px;
    min-height: 450px;
    background-color: transparent;
    box-shadow: 0px 0px 4px rgba(255, 255, 255, 0.5);
    margin-top: 40px;
    border-radius: 8px;
    padding: 20px;
    display: flex;
    flex-direction: column;
    row-gap: 25px;
}

.header {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.contents {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    row-gap: 14px;
}
</style>
