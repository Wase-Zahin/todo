have to pass the projects array to main-section
have to pass the showProjects methos from main-section to here.

<template>
    <div class="projectItems">
        <h3>Projects</h3>
        <ul>
            <li @click="showProject" v-for="item in projects" :key="item.id">
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
        
    },
    data() {
        return {
            toggleProjects: false,
            projects: [
                { id: uniqueId('project-'), label: 'This is a project' }
            ]
        }
    },
    methods: {
        addProject(labelData) {
            this.projects.push({ id: uniqueId('todo-'), label: labelData });
        },
        deleteProject(id) {
            for (let i = 0; i < this.projects.length; i++) {
                if (this.projects[i].id === id) {
                    this.projects.splice(i, 1);
                }
            }
        },
        showProject() {
            this.$emit('show-projects', this.projects, this.toggleProjects);
        }
    }
}

</script>
  