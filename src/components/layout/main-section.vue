<template>
    <main>
        <!-- this is the navigation bar -->
        <nav v-if="showMenu">
            <button @click="showInbox" ><img src="../images/email-check.png" alt="inbox" /> Inbox</button>
            <button @click="showProjects"><img src="../images/star-outline.png" alt="bookmark" />Bookmarks</button>
            <!-- navigation for projects -->
            <navProjects></navProjects>
        </nav>

        <!-- todo items to show in the main section of the page -->
        <div v-if="this.toggleInbox" class="toDoItems">
            <h2>Inbox</h2>
            <ul>
                <li v-for="item in inboxItems" :key="item.id">
                    <ToDoItemVue @todo-deleted="deleteInboxItems" :label="item.label" :id="item.id">
                    </ToDoItemVue>
                </li>
            </ul>
            <ToDoForm @todo-added="addInboxItems"></ToDoForm>
        </div>

        <div v-if="this.toggleProjects" class="toDoItems">
            <h2>Projects</h2>
            <ul>
                <li v-for="item in projects" :key="item.id">
                    <ToDoItemVue @todo-deleted="deleteProjectItems" :label="item.label" :id="item.id">
                    </ToDoItemVue>
                </li>
            </ul>
            <ToDoForm @todo-added="addProjects"></ToDoForm>
        </div>
    </main>
</template>

<script>
// this component handles all the todo items shown in the page
// arrays and methods for the todo items for each project, inbox or
// bookmark items are defined here
import ToDoForm from "../utils/ToDoForm.vue"
import ToDoItemVue from '../utils/ToDoItem.vue';
import navProjects from '../navigate/navProjects.vue';
// import navBookmarks from '../navigate/navBookmarks.vue';
import uniqueId from 'lodash.uniqueid'

export default {
    name: 'main-section',
    components: {
        ToDoItemVue,
        ToDoForm,
        navProjects
    },
    props: {
        showMenu: {
            type: Boolean
        }
    },
    data() {
        return {
            toggleInbox: true,
            toggleProjects: false,
            inboxItems: [
                { id: uniqueId('todo-'), label: '', done: false }
            ],
            projects: [
                { id: uniqueId('project-'), label: '' }
            ]
        }
    },
    methods: {
        addInboxItems(labelData) {
            this.inboxItems.push({ id: uniqueId('todo-'), label: labelData, done: false });
        },
        addProjects(labelData) {
            this.projects.push({ id: uniqueId('todo-'), label: labelData, done: false });
        },

        deleteInboxItems(id) {
            for (let i = 0; i < this.inboxItems.length; i++) {
                if (this.inboxItems[i].id === id) {
                    this.inboxItems.splice(i, 1);
                    return;
                }
            }
        },
        deleteProjectItems(id) {
            for (let i = 0; i < this.projects.length; i++) {
                if (this.projects[i].id === id) {
                    this.projects.splice(i, 1);
                    return;
                }
            }
        },
        showInbox() {
            this.toggleInbox = true;
            this.toggleProjects = false;
        },
        showProjects() {
            this.toggleInbox = false;
            this.toggleProjects = true;
        }
    }
}

</script>