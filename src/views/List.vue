<template>
  <div class='form'>
    <!-- Input -->
    <AddTask/>
    <br>

    <!-- List -->
    <form v-for="(value, id) in $parent.$data.base" :key="id">
      <router-link 
        :to="{ name: 'Edit', params: id}"
      >
       <h2>
          {{ value.taskTitle }}
          <ion-icon class="trash" name="trash"
            @mouseenter="$event.target.style.color = '#999'"
            @mouseleave="$event.target.style.color = '#ddd'"
            @click.prevent="() => deleteTask(index)"
          ></ion-icon>
        </h2>
      </router-link>
      <ul v-for="(todo, i) in value.todos.slice(0,2)" :key="i">
        <li>
          <span type="text">
            <strong>{{ i + 1 }}</strong>
            {{todo.title}}
            <input v-if="todo.completed" type="checkbox" checked disabled/>
            <input v-else type="checkbox" disabled/>
          </span>
        </li>
      </ul>
      <br>
    </form>
  </div>
</template>

<script>
import AddTask from '@/components/AddTask'
export default {
  data() {
    return {

    }
  },
  components: {
    AddTask,
  },
  methods: {
    deleteTask(id) {
      this.$parent.$data.base.splice(id, 1)
      localStorage.setItem("myBase", JSON.stringify(this.$parent.$data.base))
    },
  }
}
</script>

<style lang="scss">
  .choosed {
    li {
      margin-bottom: 5px;
      border:1px solid #ccc;
      display: flex;
      justify-content: space-between;
    }
    .done {
      text-decoration: line-through;
    }
    input {
      margin-right: 1rem;
      position: static; 
    }
  }
  ul{
    list-style-type: none;
    padding-left:10px
    
  }
  .form{
    font-family: 'Open Sans Condensed';
    width: 500px;
    padding: 30px;
    background: #FFFFFF;
    margin: 50px auto;
    box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.22);
    -moz-box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.22);
    -webkit-box-shadow:  0px 0px 15px rgba(0, 0, 0, 0.22);
  }
  .form h2{
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    background: #333;
    text-transform: uppercase;
    font-family: 'Open Sans Condensed', sans-serif;
    color: #ddd;
    font-size: 18px;
    font-weight: 100;
    padding: 15px;
    margin: -30px -30px 0px -30px;
  }
  .form span[type="text"]
  {
    display: flex;
    align-items: center;
    justify-content: space-between;
    box-sizing: border-box;
    outline: none;
    width: 100%;
    border: none;
    border-bottom: 1px solid #ddd;
    background: transparent;
    padding-bottom: 0px;
    font: 16px Arial, Helvetica, sans-serif;
    height: 60px;
    overflow: hidden;
  }
  .form input[type="checkbox"] {
    margin-bottom: 10px;
    height: 14px;
  }
  ion-icon.trash {
    position:absolute;
    font-size: 22px;
    margin-left: 240px;
    cursor: pointer;
  }
    
</style>