<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" placeholder="일정을 입력하세요." @keyup.enter="addTodo" />
    <span class="addContainer" @click="addTodo" style="cursor:pointer">
      <i class="addBtn fas fa-plus" aria-hidden="true"></i>
    </span>
    <modal v-if="showModal" @close="showModal = false">
      <h3 slot="header">경고</h3>
      <span slot="footer" @click="showModal = false">
        할 일을 입력하세요.
        <i class="closeModalBtn fas fa-times" aria-hidden="true"></i>
      </span>
    </modal>
  </div>
</template>

<script>
  import Modal from '@/components/common/Modal.vue';
  export default {
    props: ['propsdata'],
    data() {
      return {
        newTodoItem: '',
        showModal: false
      };
    },
    components: {
      Modal
    },
    methods: {
      addTodo() {
        if (this.newTodoItem !== '') {
          var value = this.newTodoItem && this.newTodoItem.trim();
          this.$emit('addTodo', value);
          this.clearInput();
        } else {
          this.showModal = !this.showModal;
        }
        console.log(this.newTodoItem);
        sessionStorage.setItem(this.newTodoItem, this.newTodoItem);
      },
      clearInput() {
        this.newTodoItem = '';
      }
    }
  };
</script>

<style scoped>
  input:focus {
    outline: none;
  }
  .inputBox {
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
  }
  .inputBox input {
    border-style: none;
    font-size: 0.9rem;
  }
  .addContainer {
    float: right;
    background: linear-gradient(to right, #6478fb, #8763fb);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
  }
  .addBtn {
    color: white;
    vertical-align: middle;
  }
</style>
