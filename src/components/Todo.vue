<template>
  <div class="todo">
    <h1>Todo</h1>

    <!-- Filter -->
    <div class="filter">
      <a href="" v-bind:class="{'actif': filter == null}" @click.prevent="filter = null">Show all</a>
      <a href="" v-bind:class="{'actif': filter == false}" @click.prevent="filter = false">Todo</a>
      <a href="" v-bind:class="{'actif': filter == true}" @click.prevent="filter = true">Completed</a>
    </div>
    <!-- End Filter -->

    <ul>
      <!-- Task -->
      <li v-show="filteredTask.length" class="todo__el" v-bind:class="{'todo__el--completed': task.completed}" v-for="(task, index) in filteredTask" :key="index" ref="todoList">
        <button class="todo__btncompleted" @click="task.completed = !task.completed">completed</button>
        <p v-if="!task.edit">{{ task.value }}</p>
        <input type="text" v-model="task.value" v-else>
        <div>
          <button @click="task.edit = !task.edit" v-show="task.edit"><i class="fas fa-check"></i></button>
          <button @click="task.edit = !task.edit" v-show="!task.edit"><i class="fas fa-edit"></i></button>
          <button @click="$emit('onRemoveEl', index)"><i class="fas fa-trash"></i></button>
        </div>
      </li>
      <!-- End Task -->

      <li v-show="!list.length" class="todo__el todo__el--add">Nothing todo</li>
      <li class="todo__el todo__el--add" @click="$emit('onAddTodo')"><i class="fas fa-plus"></i></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Todo',
  props: {
    list: Array
  },
  data () {
    return {
      filter: null
    }
  },
  computed: {
    filteredTask () {
      const f = this.list.filter(el => el.completed === this.filter)

      return this.filter !== null ? f : this.list
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .todo{
    .filter{
      display: flex;
      justify-content: space-around;
      border-radius: 5px 5px 0 0;
      border: 1px solid #ededed;
      overflow: hidden;
      & a{
        text-decoration: none;
        background: #FFF;
        display: block;
        width: 100%;
        height: 50px;
        line-height: 50px;
        text-align: center;
        margin-bottom: 0;
        color: #3B4958;
        &.actif{
          background: #F6F6F6;
        }
      }
    }
    & ul {
      margin-top: 0;
      width: 300px;
      border-radius: 0 0 5px 5px;
      border: 1px solid #ededed;
      padding: 0;
      box-shadow:
        0 4.5px 3.6px rgba(0, 0, 0, 0.024),
        0 12.5px 10px rgba(0, 0, 0, 0.035),
        0 30.1px 24.1px rgba(0, 0, 0, 0.046),
        0 100px 80px rgba(0, 0, 0, 0.07)
      ;
    }

    &__el{
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 10px;
      transition: background .15s ease-in-out;
      background: #fff;

      p,input{
        margin: 5px 0;
        width: 180px;
        margin-left: 10px;
      }

      input{
        margin: 5px 0;
        font-size: 16px;
        border: none;
        border-bottom: 1px solid #ededed;
        background: none;
      }

      &:hover{
        background: #efefef;
      }

      &+ .todo__el{
        border-top: 1px solid #ededed;
      }
    }

    &__el--add{
      justify-content: center;
      padding: 20px 10px;
      cursor: pointer;
    }
    &__el--completed {
      p{
        text-decoration: line-through;
        opacity: .5;
      }
      & .todo__btncompleted:after{
        opacity: 1;
      }
    }
    &__btncompleted {
      width: 30px;
      height: 30px;
      border-radius: 50%;
      text-indent: -9999px;
      position: relative;
      outline: none;
      &:after{
        content: "";
        width: 100%;
        height: 100%;
        background: url(../assets/check-solid.svg) no-repeat center;
        background-size: 50%;
        opacity: .1;
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%)
      }
    }
  }
</style>
