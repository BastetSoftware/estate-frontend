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

    import { SendAPICall } from "$lib/API.svelte";
    import { onMount } from "svelte";
    import { get } from "svelte/store";
    //import { page } from "$app/stores";
    import { storage } from "$lib/Storage";

    class Structure {
        constructor(arg = {}) {
            this.files = [];
            this.name = "";
            this.type = "";
            this.desc = "";
            this.district = "";
            this.region = "";
            this.area = {};
            this.owner = "";
            this.address = "";
            this.state = "";
            this.actual_user = "";

            if (arg != {}) {
                for (var attrname in arg) {
                    this[attrname] = arg[attrname];
                }
            }
        }
    }

    let objs = [];

    onMount(async () => {
        var objData = await SendAPICall("find_object", {
            Token: get(storage).token,
            Limit: 50,
        });

        if (objData.Code) {
            alert(`Произошла ошибка (${objData.Code}).`);
            return;
        }

        objs = objData.Structures;
    });
</script>

<svelte:head>
    <title>Home</title>
    <meta name="description" content="Svelte demo app" />
</svelte:head>

<div class="w-full p-5 pb-0">
    <h1 class="ml-0 mr-3">Список объектов</h1>
    <p class="m-0 p-0 text-gray-400">сводная таблица, быстрый поиск</p>
</div>
<div class="p-5 w-full flex flex-col lg:flex-row gap-x-3 gap-y-3">
    <div class="w-full">
        <Table shadow>
            <TableHead>
                <TableHeadCell>Название</TableHeadCell>
                <TableHeadCell>Адрес</TableHeadCell>
                <TableHeadCell>Район</TableHeadCell>
                <TableHeadCell>Округ</TableHeadCell>
                <TableHeadCell>Тип объекта</TableHeadCell>
                <TableHeadCell>Площадь</TableHeadCell>
                <TableHeadCell>Состояние</TableHeadCell>
                <TableHeadCell>Собственник</TableHeadCell>
                <TableHeadCell>Фактич. пользователь</TableHeadCell>
            </TableHead>
            <TableBody>
                {#each objs as strct}
                    <TableBodyRow>
                        <TableBodyCell><a href="/object/{strct.Id}">{strct.Name}</a></TableBodyCell>
                        <TableBodyCell>{strct.Address}</TableBodyCell>
                        <TableBodyCell>{strct.Region}</TableBodyCell>
                        <TableBodyCell>{strct.District}</TableBodyCell>
                        <TableBodyCell>{strct.Type}</TableBodyCell>
                        <TableBodyCell>{strct.Area} м²</TableBodyCell>
                        <TableBodyCell>{strct.State}</TableBodyCell>
                        <TableBodyCell>{strct.Owner}</TableBodyCell>
                        <TableBodyCell>{strct.Actual_user}</TableBodyCell>
                    </TableBodyRow>
                {/each}
                <!---->
            </TableBody>
        </Table>
    </div>
</div>
