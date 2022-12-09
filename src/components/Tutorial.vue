<template>
  <div>
    <table>
      <!-- テーブルヘッダー -->
      <thead>
      <tr>
        <th class="id">ID</th>
        <th class="comment">コメント</th>
        <th class="state">状態</th>
        <th class="button">-</th>
      </tr>
      </thead>
      <tbody>
        <!-- ここに<tr>でToDoの要素を1行ずつ表示 -->
        <tr v-for="todoItem in todos" v-bind:key="todoItem.id">
          <td>{{ todoItem.id }}</td>
          <td>{{ todoItem.comment }}</td>
          <td class="buttonChangeState">
            <button>{{ todoItem.state }}</button>
          </td>
          <td class="buttonDelete">
            <button>削除</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'Tutorial',
  data () {
    return {
      todos: []
    }
  }
}
</script>

<style scoped>
</style>