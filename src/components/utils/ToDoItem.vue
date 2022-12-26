<template>
    <div>
        <input type="checkbox" :id="id" :checked="!isDone"/>
        <label :for="id">{{ label }}
        </label>
    </div>
    <div>
        <input @click="console" class="todoBookmark" type="checkbox" :checked="isBookmarked">
        <img @click="onDelete" src="../images/delete.png" alt="delete" />
    </div>
</template>

<script>

export default {
    props: {
        label: { required: true, type: String },
        done: { default: true, type: Boolean },
        id: { required: true, type: String },
        bookmarked: { default: false, type: Boolean}
    },
    data() {
        return {
            isDone: this.done,
            isBookmarked: this.bookmarked
        }
    },
    methods: {
        onDelete() {
            this.$emit("todo-deleted", this.id);
        },
        console() {
            this.$emit("update-array", this.id)
        }
    }
}
</script>