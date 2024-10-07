<template>
  <div id="app">
    <h1>Sticker Packer</h1>
    <p v-if="username">Привет, {{ username }}!</p>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted } from 'vue';

export default defineComponent({
  name: 'App',
  setup() {
    const username = ref<string | null>(null);

    onMounted(() => {
      // Проверяем наличие Telegram Web App SDK
      const tg = window.Telegram.WebApp;
      if (tg) {
        tg.ready(); // Сообщаем Telegram, что приложение готово
        // Получаем информацию о пользователе, если она доступна
        const user = tg.initDataUnsafe?.user;
        if (user) {
          username.value = user.first_name; // Присваиваем имя пользователя
        }
      }
    });

    return {
      username,
    };
  }
});
</script>

<style scoped>
#app {
  text-align: center;
  margin-top: 100px;
  font-family: Arial, sans-serif;
}
</style>
