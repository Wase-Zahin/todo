<template>
    <main>
        <nav v-if="menuClicked">
            <button><img src="../images/email-check.png" alt="inbox" /> Inbox</button>
            <button><img src="../images/star-outline.png" alt="bookmark" />Bookmarks</button>
            <h3>Projects</h3>
        </nav>

        <div class="projectItems">
            <h2>Inbox</h2>
            <ul>
                <li v-for="item in ToDoItems" :key="item.id">
                    <ToDoItemVue @todo-deleted="deleteToDo" :label="item.label" :done="item.done" :id="item.id">
                    </ToDoItemVue>
                </li>
            </ul>
            <ToDoForm @todo-added="addToDo"></ToDoForm>
        </div>
    </main>
</template>

<script>
import ToDoForm from "../utils/ToDoForm.vue"
import ToDoItemVue from '../utils/ToDoItem.vue';
import uniqueId from 'lodash.uniqueid'

export default {
    name: 'main-section',
    components: {
        ToDoItemVue,
        ToDoForm,
    },
    props: {
        menuClicked: {
            type: Boolean
        }
    },
    data() {
        return {
            ToDoItems: [
                { id: uniqueId('todo-'), label: '', done: false }
            ]
        }
    },
    methods: {
        addToDo(labelData) {
            this.ToDoItems.push({ id: uniqueId('todo-'), label: labelData, done: false });
        },
        deleteToDo(id) {
            for (let i=0; i < this.ToDoItems.length; i++) {
                if (this.ToDoItems[i].id === id) {
                    this.ToDoItems.splice(i, 1);
                }
            }
        }
    }
}

</script>