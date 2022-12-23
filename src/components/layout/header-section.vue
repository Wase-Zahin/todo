<template>
    <header>
        <h1>Todo</h1>

        <img src="../images/menu.png" @click="onClick" alt="menu" />
    </header>
</template>

<script>

export default {
    methods: {
        onClick() {
            this.$emit("toggle-menu");
        }
    }
}
</script>