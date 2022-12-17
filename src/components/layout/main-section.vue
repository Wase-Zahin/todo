<template>
    <main>
        <!-- this is the navigation bar -->
        <nav v-if="menuClicked">
            <button><img src="../images/email-check.png" alt="inbox" /> Inbox</button>
            <button><img src="../images/star-outline.png" alt="bookmark" />Bookmarks</button>
            <!-- navigation for projects -->
            <navProjects></navProjects>
        </nav>

        <!-- todo items to show in the main section of the page -->
        <div class="toDoItems">
            <h2>Inbox</h2>
            <ul>
                <li v-for="item in inboxItems" :key="item.id">
                    <ToDoItemVue @todo-deleted="deleteInboxItems" :label="item.label" :id="item.id">
                    </ToDoItemVue>
                </li>
            </ul>
            <ToDoForm @todo-added="addInboxItems"></ToDoForm>
        </div>

        <div class="toDoItems">
            <h2>Projects</h2>
            <ul>
                <li v-for="item in projectItems" :key="item.id">
                    <ToDoItemVue @todo-deleted="deleteProjectItems" :label="item.label" :id="item.id">
                    </ToDoItemVue>
                </li>
            </ul>
            <ToDoForm @todo-added="addProjectItems"></ToDoForm>
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
        menuClicked: {
            type: Boolean
        }
    },
    data() {
        return {
            inboxItems: [
                { id: uniqueId('todo-'), label: '', done: false }
            ],
            projectItems: [
                { id: uniqueId('project-'), label: '' }
            ]
        }
    },
    methods: {
        addInboxItems(labelData) {
            this.inboxItems.push({ id: uniqueId('todo-'), label: labelData, done: false });
        },
        addProjectItems(labelData) {
            this.projectItems.push({ id: uniqueId('todo-'), label: labelData, done: false });
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
            for (let i = 0; i < this.projectItems.length; i++) {
                if (this.projectItems[i].id === id) {
                    this.projectItems.splice(i, 1);
                    return;
                }
            }
        },
    }
}

</script>