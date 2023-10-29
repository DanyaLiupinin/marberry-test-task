<template>
    <div class="block">
        <div class="unloadDetails">
            <div class="unloadDetails__header">
                <div class="unloadDetails__id">
                    <p>{{ removeHtmlTags(selectedCard.id) }}</p>
                </div>
                <p class="unloadDetails__title">{{ removeHtmlTags(selectedCard.event) }}</p>
                <button
                class="unloadDetails-close-btn unloadDetails-close-btn_desktop" type="button"
                    @click="closeUnloadDetails">
                    <img src="../../assets/images/icons/close-button.png" alt="close" />
                </button>
            </div>
            <div class="unloadDetails__main-block">
                <div class="unloadDetails__warning">
                    <img src="../../assets/images/icons/light-icon.png" alt="light" />
                    <p>Если после клика на ссылку загрузка не пошла, проверьте, не блокирует ли браузер скачивание архива
                    </p>
                </div>
                <p class="text-bold unloadDetails__link-caption">Cсылка для скачивания архива выгрузки (.zip)</p>
                <div class="unloadDetails__link-container">
                    <a class="link" :href="downloadLink">{{ downloadLink }}</a>
                    <span class="span-link" @click="copyText">cкопировать ссылку</span>
                </div>
                <div class="unloadDetails-close-btn-wrapper">
                    <button 
                    class="unloadDetails-close-btn unloadDetails-close-btn_mob" type="button"
                        @click="closeUnloadDetails">
                        Закрыть
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        selectedCard: {
            type: Object,
            default: () => ({})
        },
        removeHtmlTags: {
            type: Function,
            default: () => input => input,
        },
    },
    emits: ["close-details"],
    computed: {
        downloadLink() {
            return this.selectedCard.id === "2175" ? "https://seenday.com/mL6OAHAEH1" : "https://seenday.com/testLink";
        }
    },
    methods: {
        copyText() {
            const text = this.downloadLink;
            const clipboardItem = new ClipboardItem({ "text/plain": new Blob([text], { type: "text/plain" }) });

            navigator.clipboard.write([clipboardItem]).catch(() => {
                alert("Не удалось скопировать текст");
            });
        },
        closeUnloadDetails() {
            this.$emit("close-details");
        },
    }
};
</script>
