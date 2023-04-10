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
        Modal,
        Fileupload,
        Spinner,
    } from "flowbite-svelte";

    import { Icon } from "@steeze-ui/svelte-icon";
    import {
        DocumentArrowUp,
        DocumentText,
        Trash,
        PlusCircle,
    } from "@steeze-ui/heroicons";

    import { DateInput, localeFromDateFnsLocale } from "date-picker-svelte";
    let date = new Date();
    import { ru } from "date-fns/locale";
    let locale = localeFromDateFnsLocale(ru);

    let countries = [
        { value: "us", name: "United States" },
        { value: "ca", name: "Canada" },
        { value: "fr", name: "France" },
    ];

    let xmlModal = false;
    let xmlLoad = 0;
    let xmlSuccess = true;
    let xmlFile = {};
    const xmlBtn = () => {
        xmlModal = true;
    };

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

    function parseXML() {
        xmlLoad = 1;

        let parser = new XMLParser();
        let file = xmlFile[0];
        let reader = new FileReader();

        reader.readAsText(file);
        reader.onload = function () {
            let tasks = parser.parse(reader.result);

            tasks = [];
            tasks.Objects.Object.forEach((element) => {
            });

            xmlLoad = 2;
            xmlSuccess = true;
        };

        reader.onerror = function () {
            console.log(reader.error);
            xmlLoad = 2;
            xmlSuccess = false;
        };
    }

    const submitBtn = async () => {
        await SubmitTask();
    };
    
    import { SendAPICall } from "$lib/API.svelte";
    import { goto } from "$app/navigation";
    import { get } from "svelte/store";
    import { storage } from "$lib/Storage";
    import { page } from "$app/stores";
    
    async function SubmitTask() {
        var length = tasks.length,
            element = null;
        for (var i = 0; i < length; i++) {
            element = tasks[i];
            console.log({
                Token: get(storage).token,
                Name: element.name.toString(),
                Description: element.desc.toString(),
                Deadline: parseInt(new Date(element.deadline.toString()).getTime().toString()),
                Status: element.status.toString(),
                Object: parseInt(element.object.toString()),
                Maintainer: parseInt(element.maintainer.toString()),
                Gid: 1,
                Permissions: 0b00111111,
            });
            var data = await SendAPICall("task_create", {
                Token: get(storage).token,
                Name: element.name.toString(),
                Description: element.desc.toString(),
                Deadline: parseInt(new Date(element.deadline.toString()).getUTCSeconds().toString()),
                Status: element.status.toString(),
                Object: parseInt(element.object.toString()),
                Maintainer: parseInt(element.maintainer.toString()),
                Gid: 1,
                Permissions: 0b00111111,
            }, `http://${$page.url.hostname}:8080/`);

           /*type ArgsFTaskCreate struct {
	Token       string
	Name        string
	Description string
	Deadline    int64
	Status      string
	Object      int64
	Maintainer  int64
	Gid         int64
	Permissions uint8
}*/
            
            if (data.Code) {
                alert(`Произошла ошибка (${data.Code}).`);
                return;
            }
        }

        alert("Данные успешно отправлены!");
        goto(`/tasks/list`);
    }

    function addTask() {
        tasks.push(new Task({}));
        tasks = tasks;
    }
</script>

<Modal title="Импорт данных" bind:open={xmlModal} permanent>
    <div class:hidden={xmlLoad != 0}>
        <Fileupload bind:files={xmlFile} />
        <Button on:click={() => {/*parseXML()*/}}>Обработать</Button>
    </div>
    <div class:hidden={xmlLoad != 1}>
        <Spinner class="mb-2" />
        <p>Обрабатываем данные. Это займёт немного времени...</p>
    </div>
    <div class:hidden={xmlLoad != 2}>
        <p class:hidden={xmlSuccess}>
            Произошла ошибка во время импорта данных.
        </p>
        <p class:hidden={!xmlSuccess}>Отлично! Данные загружены.</p>
    </div>
    <svelte:fragment slot="footer">
        <div class:hidden={xmlLoad == 1}>
            <Button
                on:click={() => {
                    xmlLoad = 0;
                    xmlFile = {};
                    xmlSuccess = true;
                    xmlModal = false;
                }}>Закрыть</Button
            >
        </div>
    </svelte:fragment>
</Modal>

<svelte:head>
    <title>Home</title>
    <meta name="description" content="Svelte demo app" />
</svelte:head>

<div
    class="w-full p-5 pb-0 grid grid-cols-1 lg:grid-cols-2 items-center gap-y-3"
>
    <div>
        <h1 class="ml-0 mr-3">Добавление задачи</h1>
        <p class="m-0 p-0 text-gray-400">
            внесение в базу данных, импорт .XML-файлов
        </p>
    </div>
    <div class="grid grid-cols-2 gap-x-3">
        <Button on:click={xmlBtn} color="dark" class="w-full"
            >Заполнить из .XML-файла <Icon
                src={DocumentText}
                class="w-4 ml-1 p-0"
            /></Button
        >
        <Button on:click={submitBtn}
            >Внести в базу <Icon
                src={DocumentArrowUp}
                class="w-4 ml-1 p-0"
            /></Button
        >
    </div>
</div>
<div class="p-5 w-full grid grid-cols-1 gap-x-3 gap-y-12">
    {#each tasks as task, i}
        <div class="w-full grid grid-cols-1 lg:grid-cols-2 gap-y-3 gap-x-3">
            <Card class="flex grow h-min min-w-full">
                <form>
                    <div
                        class="grid grid-cols-1 lg:grid-cols-2 gap-x-3 gap-y-3 text-zinc-800"
                    >
                        <div class="flex flex-row gap-x-3 w-full lg:col-span-2">
                            <div class="w-full">
                                <Input
                                    placeholder="Название"
                                    id="name"
                                    name="name"
                                    type="text"
                                    bind:value={task.name}
                                />
                            </div>

                            <Button
                                color="red"
                                on:click={() => {
                                    tasks.splice(i, 1);
                                    tasks = tasks;
                                }}><Icon src={Trash} class="w-4" /></Button
                            >
                        </div>
                        <div class="flex flex-col gap-y-3">
                            <Select
                                placeholder="Статус"
                                items={countries}
                                bind:value={task.status}
                            />
                            <Input
                                id="maintainer"
                                name="floating_outlined"
                                type="number"
                                placeholder="Ответственный"
                                bind:value={task.maintainer}
                            />
                        </div>
                        <div class="flex flex-col gap-y-3">
                            <Input
                                id="obj"
                                name="floating_outlined"
                                type="number"
                                placeholder="Объект"
                                bind:value={task.object}
                            />
                            <Input
                                id="obj"
                                name="floating_outlined"
                                type="date"
                                placeholder="Срок сдачи"
                                bind:value={task.deadline}
                            />
                        </div>
                    </div>
                </form>
            </Card>
            <Card class="flex grow h-min min-w-full">
                <form>
                    <div
                        class="grid grid-cols-1 lg:grid-cols-2 gap-x-3 gap-y-3 text-zinc-800"
                    >
                        <Textarea
                            id="desc"
                            placeholder="Описание"
                            bind:value={task.desc}
                            class="lg:col-span-2"
                        />
                    </div>
                </form>
            </Card>
        </div>
    {/each}
</div>
<div class="w-full flex justify-center mb-3">
    <Button on:click={() => addTask()}
        >Добавить<Icon src={PlusCircle} class="w-4 ml-1 p-0" /></Button
    >
</div>
