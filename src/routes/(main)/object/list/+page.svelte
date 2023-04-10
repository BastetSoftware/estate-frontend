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
        Pagination,
        PaginationItem,
    } from "flowbite-svelte";

    import { Icon } from "@steeze-ui/svelte-icon";
    import {
        DocumentArrowDown,
        DocumentText,
        Trash,
        PlusCircle
    } from "@steeze-ui/heroicons";

    import { SendAPICall } from "$lib/API.svelte";
    import { onMount } from "svelte";
    import { get } from "svelte/store";
    import { page } from "$app/stores";
    import { storage } from "$lib/Storage";

    let pagelist = 0;
    
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
    
    async function loadObjs() {
        var objData = await SendAPICall("find_object", {
            Token: get(storage).token,
            Limit: 20,
            Offset: 20*pagelist
        }, `http://${$page.url.hostname}:8080/`);

        if (objData.Code) {
            alert(`Произошла ошибка (${objData.Code}).`);
            return;
        }
        
        return objData.Structures;
    }
    
    onMount(async () => {objs = await loadObjs()});
    
    const previousBtn = async () => {
        if (pagelist > 0) {
            pagelist -= 1;
            objs = await loadObjs();
        }
    }
    
    const nextBtn = async () => {
        if (objs.length < 20) { return }
        pagelist += 1;
        var data = await loadObjs();
        if (data.length != 0) {
            objs = data;
        } else {
            pagelist -= 1;
        }
    }
</script>

<svelte:head>
    <title>Home</title>
    <meta name="description" content="Svelte demo app" />
</svelte:head>

<div class="w-full p-5 pb-0">
    <h1 class="ml-0 mr-3">Список объектов</h1>
    <p class="m-0 p-0 text-gray-400">сводная таблица, быстрый поиск</p>
</div>
<div class="p-5 w-full flex flex-col gap-x-3 gap-y-3">
    <div class="flex justify-center items-center w-full space-x-3">
        <PaginationItem on:click={previousBtn}>Назад</PaginationItem>
        <p class="text-sm text-gray-500">Страница {pagelist + 1}</p>
        <PaginationItem on:click={nextBtn}>Вперёд</PaginationItem>
      </div>
    <div class="w-full">
        <Table shadow>
            <TableHead>
                <TableHeadCell>ID</TableHeadCell>
                <TableHeadCell>Название</TableHeadCell>
                <TableHeadCell>Адрес</TableHeadCell>
                <TableHeadCell>Регион</TableHeadCell>
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
                        <TableBodyCell>{strct.Id}</TableBodyCell>
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
