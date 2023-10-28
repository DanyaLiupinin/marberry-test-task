<template>
  <div class="unload">
    <div class="blocks">
      <Info-block title="Выгрузка" subtitle="Выполняет работу">
        <p>- собирает фотографии из заказов пользователей</p>
        <p>- собирает фотографии из заказов пользователей</p>
      </Info-block>

      <div v-for="(item, index) in response" :key="index" class="block">
        <p>Задача выполнена: <span class="text-bold">{{ item.date }}</span></p>

        <p>
          Статус выдачи: <span class="text-bold">{{ item.status_text }}</span>
        </p>
        <p>
          ID выгрузки: <span class="text-bold">{{ item.id }}</span>
        </p>
      </div>
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
import InfoBlock from "./InfoBlock.vue";
import { useAPIFetch } from "#imports";

const response = ref([]);

const fetchData = async () => {
      try {
        const { data } = await useAPIFetch('https://dev-cabinet.seenday.com/e.scripts?page=pages:unload&event=get');
        
        response.value = JSON.parse(data.value).response.data; 
      } catch (error) {
        console.error(error);
      };
    }

onMounted(() => {
  setTimeout(async () => {
    await fetchData()
  }, 0)

})
</script>