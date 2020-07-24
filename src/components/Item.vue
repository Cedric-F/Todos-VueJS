


<template>
    <div class="item" v-bind:class="{'done':this.completed}" @click="handleClick">
        <div class="editor">
            <div v-if="!this.editing" class="title">{{this.title}}</div>
            <form class="edit" @submit.prevent v-else>
                <input class="field" type="text" v-model="this.title">
                <button class="confirm"><i class="fas fa-check" /></button>
            </form>
        </div>
        <i class="fas fa-trash-alt" title="Delete item" @click="deleteItem"></i>
    </div>
</template>

<script>
    export default {
        name: "Item",
        data: (() => ({
            editing: false
        })),
        props: {
            _id: String,
            title: String,
            completed: Boolean
        },
        methods: {
            deleteItem(e) {
                e.target.classList.contains("fa-trash-alt") && this.$emit('delete', this._id);
            },
            handleClick(e) {
                const { _id, title, completed } = this;
                const item = {
                    _id,
                    title,
                    completed: !completed
                };

                !e.target.classList.contains("fas") && this.$emit('toggle', item);
            }
        }
    }
</script>

<style scoped>
    div.item {
        cursor: pointer;
        display: flex;
        align-items: center;
        justify-content: center;
        position: relative;
        width: 100%;
        height: 100px;
        background: darkred;
        color: white;
        user-select: none;
    }

    div.item:nth-child(even) {
        filter: hue-rotate(15deg);
    }

    div.item.done {
        background: darkgreen;
    }

    div.editor {
        display: flex;
        width: 100%;
        justify-content: center;
        align-items: center;
    }

/*    div.editor::before {
        content: '\f040';
        font: normal normal normal 1rem/1 FontAwesome;
    }*/

    div.title,
    form.edit {
        width: 50%;
        position: relative;
    }

    form.edit .confirm {
        position: absolute;
        top: 5px;

    }

    form.edit .confirm {
        content: '\f00c';
        font: normal normal normal 1rem/1 FontAwesome;
        background: transparent;
        border: none;
    }

    form.edit input[type="text"] {
        background: none;
        border: none;
        border-bottom: 2px solid white;
        color: white;
        font-family: inherit;
        font-size: 1rem;
        padding: 8px;
        height: 100%;
        width: 100%;
    }

    .fa-trash-alt {
        position: absolute;
        bottom: 10px;
        right: 15px;
        font-size: 12px;
        font-weight: bold;
        padding: 3px;
    }
</style>