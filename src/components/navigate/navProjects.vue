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
    data() {
        return {
            projects: [],
            toggleProject: false,
            currentProjectName: '',
            currentId: '',
            projectOnFocus: '',
        }
    },
    methods: {
        addProject(labelData) {
            this.projects.push({ id: uniqueId('project-'), label: labelData, projectToDo: [] });
        },
        deleteProject(id) {
            for (let i = 0; i < this.projects.length; i++) {
                if (this.projects[i].id === id) {
                    this.projects.splice(i, 1);
                    // reset
                    this.projectOnFocus = '';
                    this.currentProjectName = '';
                }
            }
        },
        showProject(e) {
            this.toggleProject = true;
            for (let i = 0; i < this.projects.length; i++) {
                if (this.projects[i].label === e.target.textContent) {
                    // extract todo array of 'projects' to pass to parent
                    this.projectOnFocus = this.projects[i].projectToDo;
                }
            }
            this.$emit('show-projects', this.projects, this.toggleProject, this.projectOnFocus, e.target.textContent);
        }
    }
}

</script>
  