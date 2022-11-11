<template>
  <q-page class="q-pa-lg">
    <h5 class="q-mt-none">О приложении</h5>
    <p>Данный приложение выполнено с целью ознакомления с Quasar: Framework.</p>
    <p>Функционал приложения:</p>
    <ul>
      <li>Добавить задачу</li>
      <li>Задача выполнена</li>
      <li>Удалить задачу(после выполнения)</li>
      <li>Сохранение статуса задач при перезагрузке страницы</li>
    </ul>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "IndexPage",
});
</script>
