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
        Accordion,
        AccordionItem
    } from "flowbite-svelte";

    import { Icon } from "@steeze-ui/svelte-icon";
    import { Telegram, Discord, Whatsapp } from "@steeze-ui/simple-icons";

    import { SendAPICall } from "$lib/API.svelte";
    import { onMount } from "svelte";
    import { get } from "svelte/store";
    import { page } from "$app/stores";
    import { storage } from "$lib/Storage";

    class Task {
        constructor(arg = {}) {
            this.name = "";
            this.desc = "";
            this.deadline = new Date();
            this.status = "";
            this.object = 0;
            this.maintainer = 0;
            this.gid = 0;
            this.permissions = 0b00110000;

            if (arg != {}) {
                for (var attrname in arg) {
                    this[attrname] = arg[attrname];
                }
            }
        }
    }

    let tasks = [new Task()];

    onMount(async () => {
        tasks = await loadTasks();
    });

    async function loadTasks() {
        var objData = await SendAPICall(
            "task_search",
            {
                Token: get(storage).token,
                Limit: 20,
                Offset: 20 * pagelist,
            },
            `http://${$page.url.hostname}:8080/`
        );

        if (objData.Code) {
            alert(`Произошла ошибка (${objData.Code}).`);
            return;
        }

        return objData.Tasks;
    }

    let pagelist = 0;

    const previousBtn = async () => {
        if (pagelist > 0) {
            pagelist -= 1;
            tasks = await loadTasks();
        }
    };

    const nextBtn = async () => {
        if (tasks.length < 20) {
            return;
        }
        pagelist += 1;
        var data = await loadTasks();
        if (data.length != 0) {
            tasks = data;
        } else {
            pagelist -= 1;
        }
    };
</script>

<svelte:head>
    <title>Home</title>
    <meta name="description" content="Svelte demo app" />
</svelte:head>

<div class="w-full p-5 pb-0">
    <h1 class="ml-0 mr-3">Список задач</h1>
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
                <TableHeadCell>Срок сдачи</TableHeadCell>
                <TableHeadCell>Статус</TableHeadCell>
                <TableHeadCell>ID объекта</TableHeadCell>
                <TableHeadCell>ID ответственного</TableHeadCell>
            </TableHead>
            <TableBody>
                {#each tasks as task}
                    <TableBodyRow>
                        <TableBodyCell>{task.Id}</TableBodyCell>
                        <TableBodyCell
                            ><a href="/task/{task.Id}">{task.Name}</a
                            ></TableBodyCell
                        >
                        <TableBodyCell>{task.Deadline}</TableBodyCell>
                        <TableBodyCell>{task.Status}</TableBodyCell>
                        <TableBodyCell>{task.Object}</TableBodyCell>
                        <TableBodyCell>{task.Maintainer}</TableBodyCell>
                    </TableBodyRow>
                {/each}
                <!---->
            </TableBody>
        </Table>
    </div>
</div>
