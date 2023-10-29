<template>
  <div class="unload">

    <section class="unload-column_first">
      <Info-block title="Выгрузка" subtitle="Выполняет работу">
        <p>- собирает фотографии из заказов пользователей</p>
        <p>- собирает фотографии из заказов пользователей</p>
      </Info-block>
      <UnloadCard
        v-for="item in response"
        :id="item.id"
        :key="item.id"
        :date="item.date"
        :status_text="item.status_text"
        :event="item.event"
        :size="item.size"
        :status="item.status === 'green' ? 1 : 2"
        :task_date="item.task_date"
        :remove-html-tags="removeHtmlTags"
        @card-clicked="showUnloadDetails(item)"
      />
    </section>

    <section class="unload-column_second">
      <div v-if="!showDetails" class="notice" data-color="light-purple">
        <p>
          Для того, чтобы просмотреть информацию о <span class="text-bold">выгрузке</span>, а также ее скачать, нажмите
          на требуемую выгрузку в столбце слева
        </p>
      </div>
      <UnloadDetails v-if="showDetails" :selected-card="selectedUnloadCard" :remove-html-tags="removeHtmlTags" @close-details="closeUnloadDetails"/>
    </section>
    
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import InfoBlock from "./UnloadInstruction.vue";
import UnloadCard from "./UnloadCard.vue";
import { useAPIFetch } from "#imports";

const response = ref([]);
const selectedUnloadCard = ref(null);
const showDetails = ref(false);

const fetchData = async () => {
  try {
    const { data } = await useAPIFetch("https://dev-cabinet.seenday.com/e.scripts?page=pages:unload&event=get");

    response.value = JSON.parse(data.value).response.data;
  } catch (error) {
    console.error(error);
  }
};

const showUnloadDetails = card => {
  selectedUnloadCard.value = { ...card };
  showDetails.value = true;
};

const closeUnloadDetails = () => {
  selectedUnloadCard.value = null;
  showDetails.value = false;
};

const removeHtmlTags = input => {
  return input.replace(/<[^>]+>/g, "");
};

onMounted(async () => {
  await nextTick();
  await fetchData();
})
</script>