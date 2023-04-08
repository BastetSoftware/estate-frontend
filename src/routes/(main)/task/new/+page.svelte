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
        Textarea,
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

    let title;
    let desc;
    let status;
    let obj;
    let maintaner;

    let deadline = new Date();

    import Flatpickr from "svelte-flatpickr";

    import "flatpickr/dist/flatpickr.css";
    import { Russian } from "flatpickr/dist/l10n/ru.js";

    const flatpickrOptions = {
        enableTime: true,
        dateFormat: "Срок сдачи: d.m.Y, H:i",
        locale: Russian,
        element: "#my-picker",
    };
</script>

<svelte:head>
    <title>Home</title>
    <meta name="description" content="Svelte demo app" />
</svelte:head>

<div class="w-full p-5 pb-0">
    <h1 class="ml-0 mr-3">Добавление задачи</h1>
    <p class="m-0 p-0 text-gray-400">
        внесение в базу данных, импорт .XML-файлов
    </p>
</div>
<div class="p-5 w-full flex flex-col lg:flex-row gap-x-3 gap-y-3">
    <div class="w-full lg:w-3/5 flex flex-col gap-y-3 h-min">
        <Card class="flex grow h-min min-w-full">
            <form>
                <Button class="bg-gray-500 w-full"
                    >Заполнить из .XML-файла <Icon
                        src={DocumentArrowUp}
                        class="w-4 ml-1 p-0"
                    /></Button
                >
                <div
                    class="grid grid-cols-1 lg:grid-cols-2 pt-3 gap-x-3 gap-y-3 text-zinc-800"
                >
                    <Input
                        placeholder="Заголовок"
                        id="title"
                        defaultClass="lg:col-span-2"
                        name="title"
                        type="text"
                        bind:value={title}
                    />
                    <div class="flex flex-col gap-y-3">
                        <Select
                            placeholder="Округ"
                            items={countries}
                            bind:value={selected}
                        />
                        <Input
                            id="maintaner"
                            name="floating_outlined"
                            type="text"
                            placeholder="Ответственный"
                            bind:value={maintaner}
                        />
                    </div>
                    <div class="flex flex-col gap-y-3">
                        <Input
                            id="obj"
                            name="floating_outlined"
                            type="text"
                            placeholder="Объект"
                            bind:value={obj}
                        />
                        <Flatpickr
                            options={flatpickrOptions}
                            bind:value={deadline}
                            element="#my-picker"
                        >
                            <div class="flatpickr" id="my-picker">
                                <input
                                    type="text"
                                    placeholder="Select Date.."
                                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                                    data-input
                                />

                                <a
                                    class="input-button"
                                    title="clear"
                                    data-clear
                                    href
                                >
                                    <i class="icon-close" />
                                </a>
                            </div>
                        </Flatpickr>
                    </div>
                    <Button class="lg:col-span-2"
                        >Внести в базу <Icon
                            src={DocumentArrowUp}
                            class="w-4 ml-1 p-0"
                        /></Button
                    >
                </div>
            </form>
        </Card>
    </div>
    <div class="w-full lg:w-2/5 flex flex-col gap-y-3 h-min">
        <Card class="flex grow h-min min-w-full">
            <form>
                <div
                    class="grid grid-cols-1 lg:grid-cols-2 gap-x-3 gap-y-3 text-zinc-800"
                >
                    <Textarea
                        id="desc"
                        placeholder="Описание"
                        bind:value={desc}
                        class="lg:col-span-2"
                    />
                </div>
            </form>
        </Card>
    </div>
</div>
