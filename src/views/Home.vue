<template>
  <div>
    <input type="text" name="name" v-model="todo"/>
    <button @click="createNewTodo">New Todo</button>
    <template v-if="todos.length > 0">
      <ul>
        <li v-for="(todo, key) in todos" :key="key">{{ todo }}</li>
      </ul>
    </template>
  </div>
</template>

<script>
  export default {
    name: "Home",
    data () {
      return {
        todo: 'Go to shopping',
        todos: [],
      }
    },
    sockets: {
      createNewTodo(newTodo) {
        this.$notification.show('New Todo', {
          body: newTodo,
          icon: 'https://png.pngtree.com/element_origin_min_pic/16/06/23/00576abea349fbf.jpg'
        }, {
          onerror () {
              console.log('Error event was called');
          },
          onclick () {
              console.log('Click event was called');
          },
          onclose () {
              console.log('Close event was called');
          },
          onshow () {
              console.log('Show event was called');
          }
        })
        this.todos.push(newTodo)
      }
    },
    methods: {
      createNewTodo(e) {
        e.preventDefault()
        if (this.todo == '') return 0
        this.$socket.emit('newTodo', this.todo)
        this.todo = ''
      }
    },
  }
</script>
