<script>
    import {
        Avatar,
        Card,
        Carousel,
        CarouselTransition,
        Table,
        TableBody,
        TableBodyCell,
        TableBodyRow,
    } from "flowbite-svelte";

    import { Icon } from "@steeze-ui/svelte-icon";
    import { Telegram, Discord, Whatsapp } from "@steeze-ui/simple-icons";

    import { SendAPICall } from "$lib/API.svelte";
    import { onMount } from "svelte";
    import { get } from "svelte/store";
    import { page } from "$app/stores";
    import { storage } from "$lib/Storage";

    let name;
    let desc;
    let deadline;
    let status;
    let object;
    let maintainer;
    let gid;
    let permissions;

    onMount(async () => {
        var objData = await SendAPICall(
            "task_get_info",
            {
                Id: parseInt($page.params.id),
                Token: get(storage).token,
            },
            `http://${$page.url.hostname}:8080/`
        );

        if (objData.Code) {
            alert(`Произошла ошибка (${objData.Code}).`);
            return;
        }

        name = objData.Name;
        desc = objData.Description;
        deadline = objData.Deadline;
        status = objData.Status;
        object = objData.Object;
        maintainer = objData.Maintainer;
    });
</script>

<svelte:head>
    <title>Home</title>
    <meta name="description" content="Svelte demo app" />
</svelte:head>

<div class="w-full p-5 pb-0">
    <h1 class="ml-0 mr-3">Карточка объекта</h1>
    <p class="m-0 p-0 text-gray-400">просмотр сведений об объекте</p>
</div>
<div class="p-5 w-full flex flex-col lg:flex-row gap-x-3 gap-y-3">
    <div class="w-full lg:w-1/2">
        <Card class="h-min text-zinc-800 min-w-full">
            <div class="text-zinc-800">
                <h4>{name}</h4>
            </div>
        </Card>
    </div>
    <div class="w-full lg:w-1/2 flex flex-col gap-y-3 h-min">
        <Card class="flex grow h-min min-w-full">
            <div class="grid grid-cols-1 gap-x-3 gap-y-3 text-zinc-800">
                <div class="flex flex-col gap-y-3">
                    <h4>Общая информация</h4>
                </div>
                <Table>
                    <TableBody>
                        <TableBodyRow>
                            <TableBodyCell
                                ><p class="font-bold">Статус</p></TableBodyCell
                            >
                            <TableBodyCell>{status}</TableBodyCell>
                        </TableBodyRow>
                        <TableBodyRow>
                            <TableBodyCell
                                ><p class="font-bold">
                                    Срок сдачи
                                </p></TableBodyCell
                            >
                            <TableBodyCell>{deadline}</TableBodyCell>
                        </TableBodyRow>
                        <TableBodyRow>
                            <TableBodyCell
                                ><p class="font-bold">
                                    ID объекта
                                </p></TableBodyCell
                            >
                            <TableBodyCell>{object}</TableBodyCell>
                        </TableBodyRow>
                        <TableBodyRow>
                            <TableBodyCell
                                ><p class="font-bold">
                                    ID ответственного
                                </p></TableBodyCell
                            >
                            <TableBodyCell>{maintainer}</TableBodyCell>
                        </TableBodyRow>
                    </TableBody>
                </Table>
                <div class="flex flex-col gap-y-3">
                    <div>
                        <b>Описание:</b>
                        <p>
                            {desc}
                        </p>
                    </div>
                </div>
            </div>
        </Card>
    </div>
</div>
