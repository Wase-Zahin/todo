<template>
    <div>
        <h1>to do</h1>
        <input type="checkbox" id="todo-item"/>
        <label for="todo-item">{{label}}</label>
    </div>
</template>

<script>

export default {
    props: {
        label: { required: true, type: String },
        done: { default: true, type: Boolean }
    }
}
</script>