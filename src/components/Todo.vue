<template>
    <div class="d-flex flex-row justify-content-between align-items-center my-2">
        <input
        v-show="isEditting"
        v-model="editText"
        class="form-control form-control-sm mr-2" type="text">
        <span
        v-show="!isEditting"
        :class="{ del : isDone }">
            {{ message }}
        </span>
        <button
        @click="saveClick"
        v-if="isEditting"
        class="btn btn-sm btn-primary" type="button">
            Save
        </button>
        <div v-else>
            <button
            @click="doneClick"
            v-if="!isDone"
            class="btn btn-sm btn-success" type="button">
                <i class="fa fa-check"></i>
            </button>
            <button
            v-if="!isDone"
            @click="editClick"
            class="btn btn-sm btn-warning mx-2" type="button">
                <i class="fa fa-edit"></i>
            </button>
            <button
            @click="removeClick"
            class="btn btn-sm btn-danger" type="button">
                <i class="fa fa-trash"></i>
            </button>
        </div>
    </div>
</template>

<style scoped>
    .del {
        text-decoration: line-through;
    }
</style>


<script>
export default {
    props: ['message'],
    data() {
        return {
            isDone: false,
            isEditting: false,
            editText: this.message
        }
    },
    methods: {
        removeClick: function() {
            this.$emit('removeTodo', this.message)
        },
        saveClick: function() {
            this.$emit('editTodo', this.message, this.editText)
            this.isEditting = false
        },
        doneClick: function() {
            this.isDone = true
        },
        editClick: function() {
            this.isEditting = true
        }
    }
}
</script>
