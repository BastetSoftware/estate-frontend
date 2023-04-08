<script>
    import {
        Avatar,
        Card,
        Table,
        TableHead,
        TableBody,
        TableBodyCell,
        TableBodyRow,
        TableHeadCell,
        TableSearch,
    } from "flowbite-svelte";

    import { Icon } from "@steeze-ui/svelte-icon";
    import {
        Telegram,
        Discord,
        Whatsapp,
        VK,
        Viber,
    } from "@steeze-ui/simple-icons";

    import { SendAPICall } from "$lib/API.svelte";
    import { onMount } from "svelte";
    import { get } from "svelte/store";

    import { storage } from "$lib/Storage";

    let name = "";
    let surname = "";
    let patronymic = "";

    let login = $page.params.id;
    import { page } from "$app/stores";

    onMount(async () => {
        var accountData = await SendAPICall("user_get_info", {
            Login: login,
            Token: get(storage).token,
        });

        name = accountData.FirstName;
        surname = accountData.LastName;
        if (accountData.Patronymic != "-") {
            patronymic = accountData.Patronymic;
        }
    });
</script>

<svelte:head>
    <title>Home</title>
    <meta name="description" content="Svelte demo app" />
</svelte:head>

<div class="w-full p-5 pb-0">
    <h1 class="ml-0 mr-3">Аккаунт</h1>
    <p class="m-0 p-0 text-gray-400">просмотр сведений об аккаунте</p>
</div>
<div class="p-5 w-full flex flex-col lg:flex-row gap-x-3 gap-y-3">
    <div class="w-full lg:w-1/3">
        <Card horizontal class="h-min text-zinc-800 min-w-full text-center">
            <div
                class="flex wrap items-center justify-center flex-col grow text-zinc-800"
            >
                <Avatar size="xl" class="mr-3 mb-3" />
                <h2>{surname} {name} {patronymic}</h2>
                <p>системный администратор</p>
                <p>логин:</p>
                <pre>{login}</pre>
            </div>
        </Card>
    </div>
    <div class="w-full lg:w-2/3 flex flex-col gap-y-3 h-min">
        <Card class="flex grow h-min min-w-full">
            <div class="grid grid-cols-1 gap-x-3 gap-y-3 text-zinc-800">
                <div class="flex flex-col gap-y-3">
                    <div>
                        <h4>{surname} {name} {patronymic}</h4>
                        <p>системный администатор</p>
                    </div>
                </div>
                <div class="flex flex-col gap-y-3">
                    <div>
                        <b>Адреса эл. почты</b>
                        <ul>
                            <li>
                                <a href="mailto:nikitin_ivan@example.com"
                                    >nikitin_ivan@example.com</a
                                >
                            </li>
                        </ul>
                    </div>
                    <div>
                        <b>Телефоны</b>
                        <ul>
                            <li><a href="tel:+79999999999">+79999999999</a></li>
                        </ul>
                    </div>
                    <div class="flex flex-row gap-x-3 gap-y-1">
                        <Icon src={Telegram} class="w-10" />
                        <Icon src={Discord} class="w-10" />
                        <Icon src={Whatsapp} class="w-10" />
                    </div>
                </div>
            </div>
        </Card>
        <Card class="flex grow h-min min-w-full">
            <div class="grid grid-cols-1 gap-x-3 gap-y-3 text-zinc-800">
                <div class="flex flex-col gap-y-3">
                    <h5>Участие в задачах</h5>
                </div>
                <div class="flex flex-col gap-y-3">
                    <Table shadow>
                        <TableHead>
                            <TableHeadCell>Задача</TableHeadCell>
                            <TableHeadCell>Объект</TableHeadCell>
                            <TableHeadCell>Роль участника</TableHeadCell>
                            <TableHeadCell>Дата прикрепления</TableHeadCell>
                        </TableHead>
                        <TableBody>
                            <TableBodyRow>
                                <TableBodyCell>Покраска стен</TableBodyCell>
                                <TableBodyCell
                                    >3-й Сетуньский проезд, 8, Москва, 119136</TableBodyCell
                                >
                                <TableBodyCell>Управляющий</TableBodyCell>
                                <TableBodyCell
                                    >6 апреля 2023, 15:22</TableBodyCell
                                >
                            </TableBodyRow>
                            <TableBodyRow>
                                <TableBodyCell>Покраска стен</TableBodyCell>
                                <TableBodyCell
                                    >3-й Сетуньский проезд, 8, Москва, 119136</TableBodyCell
                                >
                                <TableBodyCell>Управляющий</TableBodyCell>
                                <TableBodyCell
                                    >6 апреля 2023, 15:22</TableBodyCell
                                >
                            </TableBodyRow>
                            <TableBodyRow>
                                <TableBodyCell>Покраска стен</TableBodyCell>
                                <TableBodyCell
                                    >3-й Сетуньский проезд, 8, Москва, 119136</TableBodyCell
                                >
                                <TableBodyCell>Управляющий</TableBodyCell>
                                <TableBodyCell
                                    >6 апреля 2023, 15:22</TableBodyCell
                                >
                            </TableBodyRow>
                        </TableBody>
                    </Table>
                </div>
            </div>
        </Card>
    </div>
</div>
