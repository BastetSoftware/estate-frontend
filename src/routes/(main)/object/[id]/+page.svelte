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

    let images = [
        {
            id: 0,
            name: "Вид снаружи",
        },
        {
            id: 1,
            name: "Фотография 2",
        },
    ];

    let showThumbs = false;

    let name;
    let type;
    let desc;
    let district;
    let region;
    let area;
    let owner;
    let address;
    let state;
    let actual_user;

    onMount(async () => {
        var objData = await SendAPICall("object_get_info", {
            Id: parseInt($page.params.id),
            Token: get(storage).token,
        });

        if (objData.Code) {
            alert(`Произошла ошибка (${objData.Code}).`);
            return;
        }

        name = objData.Name;
        type = objData.Type;
        desc = objData.Description;
        district = objData.District;
        region = objData.Region;
        area = objData.Area;
        owner = objData.Owner;
        address = objData.Address;
        state = objData.State;
        actual_user = objData.Actual_user;
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
                <p>{address}</p>
            </div>
            <Carousel {images} {showThumbs} />
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
                                ><p class="font-bold">Адрес</p></TableBodyCell
                            >
                            <TableBodyCell>{address}</TableBodyCell>
                        </TableBodyRow>
                        <TableBodyRow>
                            <TableBodyCell
                                ><p class="font-bold">Округ</p></TableBodyCell
                            >
                            <TableBodyCell>{district}</TableBodyCell>
                        </TableBodyRow>
                        <TableBodyRow>
                            <TableBodyCell
                                ><p class="font-bold">Район</p></TableBodyCell
                            >
                            <TableBodyCell>{region}</TableBodyCell>
                        </TableBodyRow>
                        <TableBodyRow>
                            <TableBodyCell
                                ><p class="font-bold">Тип</p></TableBodyCell
                            >
                            <TableBodyCell>{type}</TableBodyCell>
                        </TableBodyRow>
                        <TableBodyRow>
                            <TableBodyCell
                                ><p class="font-bold">Площадь</p></TableBodyCell
                            >
                            <TableBodyCell>{area} м²</TableBodyCell>
                        </TableBodyRow>
                        <TableBodyRow>
                            <TableBodyCell
                                ><p class="font-bold">
                                    Собственник
                                </p></TableBodyCell
                            >
                            <TableBodyCell>{owner}</TableBodyCell>
                        </TableBodyRow>
                        <TableBodyRow>
                            <TableBodyCell
                                ><p class="font-bold">
                                    Пользователь
                                </p></TableBodyCell
                            >
                            <TableBodyCell>{actual_user}</TableBodyCell>
                        </TableBodyRow>
                        <TableBodyRow>
                            <TableBodyCell
                                ><p class="font-bold">
                                    Состояние
                                </p></TableBodyCell
                            >
                            <TableBodyCell>{state}</TableBodyCell>
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
