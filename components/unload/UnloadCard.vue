<template>
    <div class="block">
        <div class="unloadCard" :class="'unloadCard_' + (props.status === 1 ? 'success' : 'danger')">
            <p>
                Задача выполнена: <span class="text-bold">{{ props.date }}</span>
            </p>
            <p>
                Статус выдачи: <span class="text-bold">{{ props.status_text }}</span>
            </p>
            <p>
                ID выгрузки: <span class="text-bold">{{ props.id }}</span>
            </p>
            <p>{{ removeHtmlTags(props.event) }}</p>
            <p>
                Размер выгрузки: <span class="text-bold">{{ props.size }}</span>
            </p>
        </div>
    </div>
</template>

<script setup>
const props = defineProps({
    date: {
        type: String,
        default: ""
    },
    // eslint-disable-next-line vue/prop-name-casing
    status_text: {
        type: String,
        default: ""
    },
    id: {
        type: String,
        default: ""
    },
    event: {
        type: String,
        default: ""
    },
    size: {
        type: String,
        default: ""
    },
    status: {
        type: Number,
        default: 1,
        validator: value => [1, 2].includes(value)
    },
    // eslint-disable-next-line vue/prop-name-casing
    task_date: {
        type: String,
        default: ""
    }
});

const removeHtmlTags = input => {
    return input.replace(/<[^>]+>/g, "");
};
</script>
