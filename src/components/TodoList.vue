<template>
    <transition-group tag="ul" name="list">
        <li v-for="(todoItem, index) in propsdata" v-bind:key="todoItem.item" class="shadow">
            <i class="checkBtn fas fa-check" v-bind:class="{checkBtnCompleted: todoItem.completed}" @click="toggleComplete(todoItem, index)"></i>
            <span v-bind:class="{textCompleted: todoItem.completed}">{{ todoItem.item }}</span>
            <span class="removeBtn" @click="removeTodo(todoItem, index)">
                <i class="fas fa-trash-alt"></i>
            </span>
        </li>
    </transition-group>
</template>

<script>
export default {
    props: ['propsdata'],

    methods: {
        removeTodo: function(todoItem, index) {
            this.$emit('removeItem', todoItem, index);
        },

        toggleComplete: function(todoItem, index) {
            this.$emit('toggleComplete', todoItem, index);
        }
    }
}
</script>

<style scope>
ul {
  list-style-type: none;
  padding-left: 0px;
  margin-top: 0;
  text-align: left;
}
li {
  display: flex;
  min-height: 50px;
  height: 50px;
  line-height: 50px;
  margin: 0.5rem 0;
  padding: 0 0.9rem;
  background: white;
  border-radius: 5px;
}
.checkBtn {
  line-height: 45px;
  color: #62acde;
  margin-right: 5px;
}
.checkBtnCompleted {
  color: #b3adad;
}
.textCompleted {
  text-decoration: line-through;
  color: #b3adad;
}
.removeBtn {
  margin-left: auto;
  color: #de4343;
}
/* transition effect */
.list-enter-active, .list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to /* .list-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}
</style>
