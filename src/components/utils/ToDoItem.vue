<template>
    <div>
        <input type="checkbox" :id="id" :checked="isDone" />
        <label :for="id">{{ label }}
        </label>
    </div>
    <div>
        <img src="../images/star-outline.png" alt="star" />
        <img @click="onDelete" src="../images/delete.png" alt="delete" />
    </div>
</template>

<script>

export default {
    props: {
        label: { required: true, type: String },
        done: { default: true, type: Boolean },
        id: { required: true, type: String }
    },
    data() {
        return {
            isDone: this.done,
        }
    },
    methods: {
        onDelete() {
            this.$emit("todo-deleted", this.id);
        }
    }
}
</script>