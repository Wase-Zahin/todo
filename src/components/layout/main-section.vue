<template>
    <div class="main">
        <nav>
            <button>Inbox</button>
            <button>Bookmarks</button>
            <h3>Projects</h3>
        </nav>

        <div class="projectItems">
            <h2>Inbox</h2>
            <ul>
                <li v-for="item in ToDoItems" :key="item.id">
                    <ToDoItemVue :label="item.label" :done="item.done" :id="item.id">
                    </ToDoItemVue>
                </li>
            </ul>
            <ToDoForm @todo-added="addToDo"></ToDoForm>
        </div>
    </div>
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
        }
    }
}

</script>