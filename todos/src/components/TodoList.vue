<template>
  <section>
    <transition-group name="list" tag="ul">
      <li v-for="(todoItem,index) in propsdata" :key="todoItem.id" class="shadow">
        <!-- <i class="checkBtn fa fa-check" aria-hidden="true"></i> -->
        <div class="input-group mb-3">
          <div class="input-group-prepend">
            <div class="input-group-text">
              <input type="checkbox" aria-label="Checkbox for following text input" v-model="todoItem.completed">
              {{ todoItem.id }}[
              {{ todoItem.created | moment('MM/DD HH:mm') }}]
              {{ todoItem.title }}
              <span class="removeBtn" type="button" @click="removeTodo(todoItem,index)">
                <i class="fa fa-trash" aria-hidden="true"></i>
              </span>              
            </div>
          </div>
        </div>
      </li>
    </transition-group>
  </section>
</template>

<script>
export default {
  props: ['propsdata'],
  // 이부분이 필요없다.
  // data() {
  //   return {
  //     todoItems: []
  //   }
  // },
  // app.vue로 옮긴다.
  // created () {
  //   if (localStorage.length > 0) {
  //     for (var i = 0; i < localStorage.length; i++) {
  //       this.todoItems.push(localStorage.key(i));
  //     }
  //   }
  // },
  methods: {
    removeTodo (todoItem, index) {
      this.$emit('removeTodo', todoItem, index);
      // localStorage.removeItem(todoItem);
      // this.todoItems.splice(index,1);
    }
  }
}
</script>

<style scoped>
  .list-enter-active, .list-leave-active {
    transition: all ls;
  }
  .list-enter, .list-leave-to {
    opacity: 0;
    transform: translateY(30px);
  }

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
    border-radius: 5px;
  }

  .checkBtn {
    line-height: 45px;
    color: #62acde;
    margin-right: 5px;
  }

  .removeBtn {
    margin-left: auto;
    color: #de4343;
  }
</style>
