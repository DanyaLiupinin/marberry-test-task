<template>
  <div class="unload">
    <div class="blocks">
      <Info-block title="Выгрузка" subtitle="Выполняет работу">
        <p>- собирает фотографии из заказов пользователей</p>
        <p>- собирает фотографии из заказов пользователей</p>
      </Info-block>

      <UnloadCard
        v-for="(item) in response"
        :id="item.id"
        :key="item.id"
        :date="item.date"
        :status_text="item.status_text"
        :event="item.event"
        :size="item.size"
        :status="item.status === 'green' ? 1 : 2"
        :task_date="item.task_date"
      />
    </div>
    <div class="notice" data-color="light-purple">
      <p>
        Для того, чтобы просмотреть информацию о <span class="text-bold">выгрузке</span>, а также ее скачать, нажмите на
        требуемую выгрузку в столбце слева
      </p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import InfoBlock from "./UnloadMainCard.vue";
import UnloadCard from "./UnloadCard.vue";
import { useAPIFetch } from "#imports";

const response = ref([]);

const fetchData = async () => {
  try {
    const { data } = await useAPIFetch("https://dev-cabinet.seenday.com/e.scripts?page=pages:unload&event=get");

    response.value = JSON.parse(data.value).response.data;

    console.log(JSON.parse(data.value).response.data);
  } catch (error) {
    console.error(error);
  }
};

onMounted(() => {
  setTimeout(async () => {
    await fetchData();
  }, 0);
});
</script>