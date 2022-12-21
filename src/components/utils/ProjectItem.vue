<template>
    <div>
        <img src="../images/todo.png" alt="star"/>
        <label :for="id">{{ label }}
        </label>
    </div>
    <div>
        <img @click="onDelete" src="../images/delete.png" alt="delete" />
    </div>
</template>

<script>

export default {
    props: {
        label: { required: true, type: String },
        id: { required: true, type: String }
    },
    methods: {
        onDelete() {
            this.$emit("project-deleted", this.id);
        }
    }
}
</script>