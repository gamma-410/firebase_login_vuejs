<template>
  <div>
    <h1>ユーザー情報</h1>
    <p>ユーザー名: {{ currentUser.displayName }}</p>
    <p>メールアドレス: {{ currentUser.email }}</p>

    <hr>

    <p>ローカルストレージのデータ: {{ currentUser }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentUser: null
    }
  },
  created() {
    const currentUser = localStorage.getItem('currentUser');
    if (currentUser) {
      this.currentUser = JSON.parse(currentUser);
    }
  }
}
</script>
