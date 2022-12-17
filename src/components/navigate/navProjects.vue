<template>
    <div class="projectItems">
    <h3>Projects</h3>
        <ul>
            <li v-for="item in projectItems" :key="item.id">
                <ProjectItem @project-deleted="deleteProject" :label="item.label" :id="item.id">
                </ProjectItem>
            </li>
        </ul>
        <ProjectForm @project-added="addProject"></ProjectForm>
    </div>

</template>
  
<script>
import ProjectForm from "../utils/ProjectForm.vue"
import ProjectItem from '../utils/ProjectItem.vue';
// import navBookmarks from '../navigate/navBookmarks.vue';
import uniqueId from 'lodash.uniqueid'

export default {
    name: 'main-section',
    components: {
        ProjectItem,
        ProjectForm,
    },
    props: {
        menuClicked: {
            type: Boolean
        }
    },
    data() {
        return {
            projectItems: [
                { id: uniqueId('project-'), label: 'This is a project' }
            ]
        }
    },
    methods: {
        addProject(labelData) {
            this.projectItems.push({ id: uniqueId('todo-'), label: labelData });
        },
        deleteProject(id) {
            for (let i = 0; i < this.projectItems.length; i++) {
                if (this.projectItems[i].id === id) {
                    this.projectItems.splice(i, 1);
                }
            }
        }
    }
}

</script>
  