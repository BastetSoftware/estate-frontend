<script>
    import {
        Avatar,
        Card,
        Carousel,
        CarouselTransition,
        Table,
        TableHead,
        TableBody,
        TableBodyCell,
        TableBodyRow,
        TableHeadCell,
        TableSearch,
    } from "flowbite-svelte";

    import { Icon } from "@steeze-ui/svelte-icon";
    import { Telegram, Discord, Whatsapp } from "@steeze-ui/simple-icons";

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
</script>

<svelte:head>
    <title>Home</title>
    <meta name="description" content="Svelte demo app" />
</svelte:head>

<div class="w-full p-5 pb-0">
    <h1 class="ml-0 mr-3">Список сотрудников</h1>
    <p class="m-0 p-0 text-gray-400">сводная таблица, быстрый поиск</p>
</div>
<div class="p-5 w-full flex flex-col lg:flex-row gap-x-3 gap-y-3">
    <div class="w-full">
        <Table shadow>
            <TableHead>
                <TableHeadCell>Адрес</TableHeadCell>
                <TableHeadCell>Координаты</TableHeadCell>
                <TableHeadCell>Тип</TableHeadCell>
                <TableHeadCell>Дата добавления</TableHeadCell>
            </TableHead>
            <TableBody>
                <TableBodyRow>
                    <TableBodyCell
                        >3-й Сетуньский проезд, 8, Москва, 119136</TableBodyCell
                    >
                    <TableBodyCell
                        ><a href="geo:55.732945,37.535763"
                            >55.732945, 37.535763</a
                        ></TableBodyCell
                    >
                    <TableBodyCell>Многоквартирный дом</TableBodyCell>
                    <TableBodyCell>6 апреля 2023, 15:22</TableBodyCell>
                </TableBodyRow>
                <TableBodyRow>
                    <TableBodyCell
                        >3-й Сетуньский проезд, 8, Москва, 119136</TableBodyCell
                    >
                    <TableBodyCell
                        ><a href="geo:55.732945,37.535763"
                            >55.732945, 37.535763</a
                        ></TableBodyCell
                    >
                    <TableBodyCell>Многоквартирный дом</TableBodyCell>
                    <TableBodyCell>6 апреля 2023, 15:22</TableBodyCell>
                </TableBodyRow><TableBodyRow>
                    <TableBodyCell
                        >3-й Сетуньский проезд, 8, Москва, 119136</TableBodyCell
                    >
                    <TableBodyCell
                        ><a href="geo:55.732945,37.535763"
                            >55.732945, 37.535763</a
                        ></TableBodyCell
                    >
                    <TableBodyCell>Многоквартирный дом</TableBodyCell>
                    <TableBodyCell>6 апреля 2023, 15:22</TableBodyCell>
                </TableBodyRow>
            </TableBody>
        </Table>
    </div>
</div>
