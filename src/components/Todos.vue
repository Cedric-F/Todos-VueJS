<template>
    <div class="items">
        <Item
            :key="item._id"
            v-for="item in items"
            v-bind:_id="item._id"
            v-bind:title="item.title"
            v-bind:completed="item.completed"
            v-on:delete="deleteItem"
            v-on:toggle="toggle"
            v-on:update="update"
        />
    </div>
</template>

<script>
    import Item from './Item.vue';

    export default {
        components: {
            Item
        },
        name: "Todos",
        props: {
            items: Array
        },
        methods: {
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
    div.items {
        overflow: auto;
    }
</style>