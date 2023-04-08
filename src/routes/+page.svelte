<script>
    import {
        Card,
        Button,
        Activity,
        ActivityItem,
        PaginationItem,
        Tabs, TabItem
    } from "flowbite-svelte";

    import { Icon } from "@steeze-ui/svelte-icon";

    import { DatePicker, localeFromDateFnsLocale } from 'date-picker-svelte';
    let date = new Date();
    import { ru } from 'date-fns/locale'
    let locale = localeFromDateFnsLocale(ru);

    import { ArrowRight } from "@steeze-ui/heroicons";

    let activities = [
        {
            title: '<span class="text-blue-500 font-bold">Петров П. Ю.</span> отправил отчёт по задаче <span class="text-blue-500 font-bold">#311 Список материалов для реставрации</span>.',
            date: "минуту назад",
            src: "",
            alt: "",
        },
        {
            title: '<span class="text-blue-500 font-bold">Иванов Г. С.</span> внёс в систему новый объект: <span class="text-blue-500 font-bold"> 3-й Сетуньский проезд, 8, Москва, 119136</span>.',
            date: "четыре минуты назад",
            src: "",
            text: "Описание: ...",
            alt: "",
        },
        {
            title: '<span class="text-blue-500 font-bold">Сидорова М. А.</span> изменила статус задачи <span class="text-blue-500 font-bold">#311 Список материалов для реставрации</span>.',
            date: "два часа назад",
            src: "",
            alt: "",
        },
    ];

    const previous = () => {
        alert(
            "Previous btn clicked. Make a call to your server to fetch data."
        );
    };
    const next = () => {
        alert("Next btn clicked. Make a call to your server to fetch data.");
    };
</script>

<svelte:head>
    <title>Home</title>
    <meta name="description" content="Svelte demo app" />
</svelte:head>

<div class="w-full p-5 pb-0">
    <h1 class="ml-0 mr-3">Главная</h1>
    <p class="m-0 p-0 text-gray-400">
        панель управления, просмотр последних событий
    </p>
</div>
<div class="p-5 w-full flex flex-col lg:flex-row gap-x-3 gap-y-3">
    <div class="w-full lg:w-1/5">
        <DatePicker bind:value={date} {locale} />
    </div>
    <div class="w-full lg:w-4/5">
        <Card class="min-w-full h-min text-zinc-800">
            <Tabs>
                <TabItem open title="Задачи">
                  <p class="text-sm text-gray-500 dark:text-gray-400"><b>Profile:</b> Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
                </TabItem>
                <TabItem title="Отчёты">
                  <p class="text-sm text-gray-500 dark:text-gray-400"><b>Settings:</b> Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
                </TabItem>
                <TabItem title="Сроки">
                  <p class="text-sm text-gray-500 dark:text-gray-400"><b>Users:</b> Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
                </TabItem>
                <TabItem title="Статистика">
                  <p class="text-sm text-gray-500 dark:text-gray-400"><b>Dashboard:</b> Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
                </TabItem>
              </Tabs>
        </Card>
    </div>
</div>