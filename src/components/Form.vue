<template>
    <div>
        <form @submit.prevent="submit">
            <input type="text" placeholder="Add a todo item..." v-model="title">
            <input type="submit" value="Add item">
        </form>
    </div>
</template>

<script>
    export default {
        name: "Form",
        data: () => ({
            title: ''
        }),
        methods: {
            submit() {
                this.title.length > 3 && this.$emit("add-item", this.title);
                this.title = '';
            }
        }
    }
</script>

<style scoped>
    form {
        display: flex;
        height: 50px;
        margin: 5px 0;
    }
    input {
        display: block;
        border: none;
    }
    input[type="text"] {
        flex: 4;
        padding-left: 15px;
        font-family: inherit;
        font-size: 16px;
    }
    input[type="submit"] {
        flex: 2;
        cursor: pointer;
        background: #42b983;
        font-family: inherit;
        color: white;
        font-size: 16px;
    }
    input[type="submit"]:active {
        background: #21a441;
    }
</style>