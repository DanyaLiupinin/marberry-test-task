<template>
    <div class="block">
        <div class="unloadDetails">
            <div class="unloadDetails__header">
                <div class="unloadDetails__id">
                    <p>10</p>
                </div>
                <p class="unloadDetails__title">{{selectedCard.event}}</p>
                <button type="button">
                    <img src="../../assets/images/icons/close-button.png" alt="close" />
                </button>
            </div>
            <div class="unloadDetails__main-block">
                <div class="unloadDetails__warning">
                    <img src="../../assets/images/icons/light-icon.png" alt="light" />
                    <p>Если после клика на ссылку загрузка не пошла, проверьте, не блокирует ли браузер скачивание архива</p>
                </div>
                <p class="text-bold unloadDetails__link-caption">Cсылка для скачивания архива выгрузки (.zip)</p>
                <div class="unloadDetails__link-container">
                    <a href="google.com">https://google.com</a>
                    <button @click="copyText">Скопировать ссылку</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>


export default {
    props: {
        selectedCard: Object
    },
    methods: {
        copyText() {
            const text = this.textToCopy || "testtest";
            const clipboardItem = new ClipboardItem({ "text/plain": new Blob([text], { type: "text/plain" }) });

            navigator.clipboard.write([clipboardItem])
            .catch(error => {
                console.log("Ошибка при копировании текста: ", error);
                alert("Не удалось скопировать текст");
            });
        }
    }
};


</script>
