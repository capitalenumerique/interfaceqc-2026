<script lang="ts" setup>
import IconExternal from '@/assets/svg/external.svg?component';

const i18nHead = useLocaleHead();

const { locale, t } = useI18n();
const config = useRuntimeConfig();
const ogImage = computed(() => `${config.public.i18n.baseUrl}/og-image-${locale.value}.png`);

const { eventDates } = useEventDates();

useHead(() => ({
    titleTemplate: (title) => {
        return title ? `${title} | Interface` : `Interface | ${eventDates.value}`;
    },
    htmlAttrs: {
        lang: i18nHead.value.htmlAttrs.lang,
    },
    link: [...(i18nHead.value.link || [])],
    meta: [
        ...(i18nHead.value.meta || []),
        {
            property: 'og:image',
            content: ogImage,
        },
    ],
}));

onBeforeMount(() => {
    useHead(() => ({
        htmlAttrs: {
            class: () => {
                const hour = new Date().getHours();
                return hour >= 9 && hour < 17 ? 'theme-day' : 'theme-night';
            },
        },
    }));
});

useSeoMeta({
    description: () =>
        t("Découvre Interface, l'événement incontournable du numérique, créé par et pour la communauté!"),
});
</script>

<template>
    <AnnouncementBar>
        {{ t("Vous consultez l’édition 2026 de l'événement.") }}
        <a :href="t('https://interfaceqc.com/')" target="_blank">
            <span>{{ t('Voir la plus récente') }}</span>
            <IconExternal />
        </a>
    </AnnouncementBar>
    <NuxtLayout>
        <NuxtLoadingIndicator :height="5" color="#333230" :throttle="500" />
        <NuxtPage />
    </NuxtLayout>
</template>

<style lang="postcss">
.page-enter-active,
.page-leave-active {
    transition: opacity 500ms ease-in-out;
}

.page-enter-from,
.page-leave-to {
    opacity: 0;
}
</style>

<i18n lang="json">
{
    "en": {
        "Découvre Interface, l'événement incontournable du numérique, créé par et pour la communauté!": "Discover Interface, the must-attend digital event created by and for the community!",
        "Vous consultez l’édition 2026 de l'événement.": "You’re viewing the 2026 edition of the event.",
        "Voir la plus récente": "View the latest",
        "https://interfaceqc.com/": "https://interfaceqc.com/en/"
    }
}
</i18n>
