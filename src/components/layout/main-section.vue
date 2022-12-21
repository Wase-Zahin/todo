<template>
    <main>
        <!-- this is the navigation bar -->
        <nav v-if="showMenu">
            <button @click="showInbox" ><img src="../images/email-check.png" alt="inbox" /> Inbox</button>
            <button @click="handler">
                <img src="../images/star-outline.png" alt="bookmark" />Bookmarks
            </button>
            <!-- navigation for projectItems -->
            <navProjects @show-projects="handler"></navProjects>
        </nav>

        <!-- todo items to show in the main section of the page -->
        <div v-if="toggleInbox" class="toDoItems">
            <h2>Inbox</h2>
            <ul>
                <li v-for="item in inboxToDo" :key="item.id">
                    <ToDoItem
                    @todo-deleted="deleteInboxItems" 
                    :label="item.label" 
                    :id="item.id">
                    </ToDoItem>
                </li>
            </ul>
            <ToDoForm @todo-added="addInboxTodo"></ToDoForm>
        </div>

        <div v-if="showProject" class="toDoItems">
            <h2>{{this.currentProjectName}}</h2>
            <ul>
                <li v-for="todo in projectOnFocus" :key="todo.id">
                    <ToDoItem
                    @todo-deleted="deleteProjectToDo" 
                    :label="todo.label" 
                    :id="todo.id">
                    </ToDoItem>
                </li>
            </ul>
            <ToDoForm @todo-added="addProjectToDo"></ToDoForm>
        </div>
    </main>
</template>

<script>
// this component handles all the todo items shown in the page
// arrays and methods for the todo items for each project, inbox or
// bookmark items are defined here
import ToDoForm from "../utils/ToDoForm.vue"
import ToDoItem from '../utils/ToDoItem.vue';
import navProjects from '../navigate/navProjects.vue';
// import navBookmarks from '../navigate/navBookmarks.vue';
import uniqueId from 'lodash.uniqueid'

export default {
    name: 'main-section',
    components: {
        ToDoItem,
        ToDoForm,
        navProjects
    },
    props: {
        showMenu: {
            type: Boolean
        },
    },
    data() {
        return {
            inboxToDo: [],
            projects: [],
            projectOnFocus: [],
            currentProjectName: '',
            showProject: false,
            toggleInbox: true,
        }
    },
    methods: {
        addInboxTodo(labelData) {
            this.inboxToDo.push({ id: uniqueId('todo-'), label: labelData, done: false });
        },
        addProjectToDo(labelData) {
            for (let i = 0; i < this.projects.length; i++) {
                if (this.projects[i].label === this.currentProjectName) {
                    this.projects[i].projectToDo.push(
                        { id: uniqueId('todo-'), label: labelData, done: false });
                }
            }
        },
        deleteInboxItems(id) {
            for (let i = 0; i < this.inboxToDo.length; i++) {
                if (this.inboxToDo[i].id === id) {
                    this.inboxToDo.splice(i, 1);
                    return;
                }
            }
        },
        deleteProjectToDo(id) {
            for (let i in this.projectOnFocus) {
                if (this.projectOnFocus[i].id === id) {
                    this.projectOnFocus.splice(i, 1);
                    console.log(this.projects);
                }
            }
        },
        showInbox() {
            this.toggleInbox = true;
            this.showProject = false;
        },
        handler(projects, showProject, projectOnFocus, currentProjectName) {
            this.toggleInbox = false;
            // extract data from child component 'navProjects'
            this.projectOnFocus = projectOnFocus
            this.showProject = showProject;
            this.projects = projects;
            this.currentProjectName = currentProjectName;
        }
    }
}

</script>