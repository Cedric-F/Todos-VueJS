<template>
    <div class="main">
        <Form v-on:add-item="addItem" />
        <Todos
            v-bind:items="this.items"
            v-on:delete="deleteItem"
            v-on:toggle="toggle"
            v-on:update="update"
        />
    </div>
</template>

<script>
    //import Item from './Item.vue';
    import Form from './Form.vue';
    import Todos from './Todos.vue';

    export default {
        name: "Main",
        components: {
            Form,
            Todos
        },
        props: {
            items: Array,
        },
        methods: {
            addItem(item) {
                this.$emit('add-item', item);
            },
            deleteItem(id) {
                this.$emit('delete', id);
            },
            toggle(item) {
                this.$emit('toggle', item);
            },
            update(item) {
                this.$emit('update', item);
            }
        }
    }
</script>

<style scoped>
    .main {
        background: #203b25;
    }
</style>