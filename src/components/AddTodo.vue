<!-- TEMPLATE / HTML --> 
<template>
    <div>
        <form @submit="addTodo">
            <input type="text" name="title" placeholder="Add Todo" v-model="title">
            <input type="submit" value="Submit" class="btn">
        </form>
    </div>
</template>

<!-- SCRIPT / JS -->
<script>
// import uuid from 'uuid'; // No ID needed as JSONplaceholder gives id itself

export default {
    name: 'AddTodo',
    data() {
        return {
            title: ''
        }
    },
    // Methods
    methods: {
        addTodo(e) {
            e.preventDefault();
            const newTodo = {
                title: this.title,
                completed: false
            }
            // Send up to parent by emitting an event
            this.$emit('add-todo', newTodo);
            // Clear Title after submitting
            this.title = '';
        }
    }
}
</script>

<!-- STYLE / CSS -->
<style scoped>
  form {
    display: flex;
  }
  input[type="text"] {
    flex: 10;
    padding: 5px;
  }
  input[type="submit"] {
    flex: 2;
  }
</style>
