<script>
    import {
        Avatar,
        Card,
        Carousel,
        CarouselTransition,
        FloatingLabelInput,
        Button,
        Select,
        Label,
        Input,
        Fileupload,
        Listgroup,
        ListgroupItem,
        Helper
    } from "flowbite-svelte";

    import { Icon } from "@steeze-ui/svelte-icon";
    import { Folder, DocumentArrowUp } from "@steeze-ui/heroicons";
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

    let selected;
    let countries = [
        { value: "us", name: "United States" },
        { value: "ca", name: "Canada" },
        { value: "fr", name: "France" },
    ];

    let files;
</script>

<svelte:head>
    <title>Home</title>
    <meta name="description" content="Svelte demo app" />
</svelte:head>

<div class="w-full p-5 pb-0">
    <h1 class="ml-0 mr-3">Добавление объектов</h1>
    <p class="m-0 p-0 text-gray-400">
        внесение в базу данных, импорт .XML-файлов
    </p>
</div>
<div class="p-5 w-full flex flex-col lg:flex-row gap-x-3 gap-y-3">
    <div class="w-full lg:w-1/2 flex flex-col gap-y-3 h-min">
        <Card class="flex grow h-min min-w-full">
            <form>
                <Button class="w-full"
                    >Заполнить из .XML-файла <Icon
                        src={DocumentArrowUp}
                        class="w-4 ml-1 p-0"
                    /></Button
                >
                <div
                    class="grid grid-cols-1 lg:grid-cols-2 pt-3 gap-x-3 gap-y-3 text-zinc-800"
                >
                    <div class="flex flex-col gap-y-3">
                        <Input
                            placeholder="Адрес"
                            id="address"
                            name="floating_outlined"
                            type="text"
                        />
                        <Select
                            placeholder="Округ"
                            items={countries}
                            bind:value={selected}
                        />
                        <Input
                            style="outlined"
                            id="patronymic"
                            name="floating_outlined"
                            type="text"
                            label="Отчество"
                        />
                    </div>
                    <div class="flex flex-col gap-y-3">
                        <Select
                            placeholder="Тип объекта"
                            items={countries}
                            bind:value={selected}
                        />
                        <FloatingLabelInput
                            style="outlined"
                            id="email"
                            name="email"
                            type="email"
                            label="Основной адрес эл. почты"
                        />
                    </div>
                </div>
            </form>
        </Card>
    </div>
    <div class="w-full lg:w-1/2 flex flex-col gap-y-3 h-min">
        <Card class="flex grow h-min min-w-full">
            <form>
                <div
                    class="grid grid-cols-1 pt-3 gap-x-3 gap-y-3 text-zinc-800"
                >
                    <div class="flex flex-col gap-y-3">
                        <h4>Прикрепление файлов</h4>
                        <Fileupload id="multiple_files" multiple bind:files />
                        <Helper>Поддерживаются картинки (.JPEG, .PNG), видеоролики (MP4, AVI, MOV), документы (.DOCX, .DOC, .ODT, .PDF), таблицы (.XLS, .XLSX)</Helper>
                        <Listgroup items={files} let:item class="mt-2">
                            {#if item}
                                {item.name}
                            {:else}
                                <ListgroupItem>Файлов нет.</ListgroupItem>
                            {/if}
                        </Listgroup>
                        
                    </div>
                </div>
            </form>
        </Card>
    </div>
</div>
