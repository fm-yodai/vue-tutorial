<template>
  <div>
    <table>
      <!-- テーブルヘッダー -->
      <thead>
      <tr>
        <th class="id">ID</th>
        <th class="comment">comment</th>
        <th class="state">state</th>
        <th class="button">-</th>
      </tr>
      </thead>
      <tbody>
        <!-- ここに<tr>でToDoの要素を1行ずつ表示 -->
        <tr v-for="todoItem in todos" v-bind:key="todoItem.id">
          <td>{{ todoItem.id }}</td>
          <td>{{ todoItem.comment }}</td>
          <td class="buttonChangeState">
            <button @click="doChangeState(todoItem)">
              {{ todoItem.state }}
            </button>
          </td>
          <td class="buttonDelete">
            <button @click="doDelete(todoItem)">
              delete
            </button>
          </td>
        </tr>
      </tbody>
    </table>

    <h2>new task</h2>
    <form class="add-form" @submit.prevent="doAdd">
      comment <input type="text" ref="comment">
      <button type="submit">add</button>
    </form>
  </div>
</template>

<script>
import todoStorage from '../plugins/todoStorage'

export default {
  name: 'Tutorial',
  data () {
    return {
      todos: [],
      uid:0
    }
  },
  created () {
    this.todos = todoStorage.fetch()
    this.uid = this.todos.length
  },
  watch: {
    todos: {
      handler: function (todos) {
        todoStorage.save(todos)
      },
      deep: true
    }
  },
  methods: {
    doAdd (event, value) {
      var comment = this.$refs.comment

      // フォームが空でAddボタンを押しても何も起こらない
      if (!comment.value.length) {
        return
      }
      this.todos.push({
        id: this.uid,
        comment: comment.value,
        state: 0
      })

      // 追加したら次の準備
      this.uid++
      comment.value = ''
    },
    doChangeState (item) {
      item.state = item.state ? 0 : 1
    },
    doDelete (item) {
      const deleteIndex = this.todos.indexOf(item)
      this.todos.splice(deleteIndex,1)
    }
  }
}
</script>

<style scoped>
</style>