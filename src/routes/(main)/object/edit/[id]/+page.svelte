<script>
    import {
        Card,
        Button,
        Select,
        Input,
        Fileupload,
        Listgroup,
        ListgroupItem,
        Helper,
        Textarea,
        Modal,
        Spinner,
    } from "flowbite-svelte";

    import { Icon } from "@steeze-ui/svelte-icon";
    import {
        DocumentArrowUp,
        DocumentText,
        Trash,
        PlusCircle,
    } from "@steeze-ui/heroicons";

    let countries = [
        { value: "us", name: "United States" },
        { value: "ca", name: "Canada" },
        { value: "fr", name: "France" },
    ];

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

    let structures = [new Structure()];

    import { SendAPICall } from "$lib/API.svelte";
    import { goto } from "$app/navigation";
    import { get } from "svelte/store";
    import { storage } from "$lib/Storage";
    import { page } from "$app/stores";
    import { onMount } from "svelte";

    onMount(async () => {
        var objData = await SendAPICall(
            "object_get_info",
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

        structures[0].name = objData.Name;
        structures[0].type = objData.Type;
        structures[0].desc = objData.Description;
        structures[0].district = objData.District;
        structures[0].region = objData.Region;
        structures[0].area = objData.Area;
        structures[0].owner = objData.Owner;
        structures[0].address = objData.Address;
        structures[0].state = objData.State;
        structures[0].actual_user = objData.Actual_user;
    });

    async function SubmitObject() {

        var element = structures[0];
        console.log({
                Token: get(storage).token,
                Name: element.name.toString(),
                Description: element.desc.toString(),
                District: element.district.toString(),
                Region: element.region.toString(),
                Address: element.address.toString(),
                Area: parseInt(element.area.toString()),
                Type: element.type.toString(),
                State: element.state.toString(),
                Owner: element.owner.toString(),
                Actual_user: element.actual_user.toString(),
                Gid: 1,
                Permissions: 255,
            });
        var data = await SendAPICall(
            "object_change",
            {
                Token: get(storage).token,
                Name: element.name.toString(),
                Description: element.desc.toString(),
                District: element.district.toString(),
                Region: element.region.toString(),
                Address: element.address.toString(),
                Area: parseInt(element.area.toString()),
                Type: element.type.toString(),
                State: element.state.toString(),
                Owner: element.owner.toString(),
                Actual_user: element.actual_user.toString(),
                Gid: 1,
                Permissions: 255,
            },
            `http://${$page.url.hostname}:8080/`
        );

        if (data.Code) {
            alert(`Произошла ошибка (${data.Code}).`);
            return;
        }

        alert("Данные успешно отправлены!");
        goto(`/object/${$page.params.id}`);
    }

    const submitBtn = async () => {
        await SubmitObject();
    };

    import { XMLParser } from "fast-xml-parser";

    let xmlModal = false;
    let xmlLoad = 0;
    let xmlSuccess = true;
    let xmlFile = {};
    const xmlBtn = () => {
        xmlModal = true;
    };

    function parseXML() {
        xmlLoad = 1;

        let parser = new XMLParser();
        let file = xmlFile[0];
        let reader = new FileReader();

        reader.readAsText(file);
        reader.onload = function () {
            let objs = parser.parse(reader.result);

            structures = [new Structure({})];
            objs.Objects.Object.forEach((element) => {
                structures[0] = new Structure({
                    files: [],
                    name: element.Name,
                    type: element.Type,
                    desc: element.Desc,
                    district: element.District,
                    region: element.Region,
                    area: element.Area,
                    owner: element.Owner,
                    address: element.Address,
                    state: element.State,
                    actual_user: element.Actual_user,
                });
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
</script>

<Modal title="Импорт данных" bind:open={xmlModal} permanent>
    <div class:hidden={xmlLoad != 0}>
        <Fileupload bind:files={xmlFile} />
        <Button on:click={() => parseXML()}>Обработать</Button>
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
        <h1 class="ml-0 mr-3">Добавление объектов</h1>
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
    {#each structures as strct, i}
        <div class="w-full grid grid-cols-1 lg:grid-cols-2 gap-y-3 gap-x-3">
            <Card class="flex grow h-min min-w-full">
                <form>
                    <div
                        class="grid grid-cols-1 lg:grid-cols-2 pt-3 gap-x-3 gap-y-3 text-zinc-800"
                    >
                        <div class="flex flex-row gap-x-3 w-full lg:col-span-2">
                            <div class="w-full">
                                <Input
                                    placeholder="Название"
                                    id="name"
                                    name="name"
                                    type="text"
                                    bind:value={strct.name}
                                />
                            </div>
                        </div>

                        <div class="flex flex-col gap-y-3">
                            <Input
                                placeholder="Адрес"
                                id="address"
                                name="floating_outlined"
                                type="text"
                                bind:value={strct.address}
                            />
                            <Select
                                placeholder="Регион"
                                items={countries}
                                bind:value={strct.region}
                            />
                            <Select
                                placeholder="Округ"
                                items={countries}
                                bind:value={strct.district}
                            />
                            <Select
                                placeholder="Тип объекта"
                                items={countries}
                                bind:value={strct.type}
                            />
                        </div>
                        <div class="flex flex-col gap-y-3">
                            <Input
                                placeholder="Площадь (м²)"
                                id="area"
                                name="floating_outlined"
                                type="number"
                                bind:value={strct.area}
                            />
                            <Input
                                placeholder="Состояние"
                                id="state"
                                name="floating_outlined"
                                type="text"
                                bind:value={strct.state}
                            />
                            <Input
                                placeholder="Собственник"
                                id="owner"
                                name="floating_outlined"
                                type="text"
                                bind:value={strct.owner}
                            />
                            <Input
                                placeholder="Фактический пользователь"
                                id="actual_user"
                                name="floating_outlined"
                                type="text"
                                bind:value={strct.actual_user}
                            />
                        </div>
                        <Textarea
                            id="desc"
                            placeholder="Описание"
                            bind:value={strct.desc}
                            class="lg:col-span-2"
                        />
                    </div>
                </form>
            </Card>
            <Card class="flex h-min min-w-full">
                <form>
                    <div class="grid grid-cols-1 gap-x-3 gap-y-3 text-zinc-800">
                        <div class="flex flex-col gap-y-3">
                            <h4>Прикрепление файлов</h4>
                            <Fileupload
                                id="multiple_files"
                                multiple
                                bind:value={strct.files}
                            />
                            <Helper
                                >Что поддерживается:<br />— картинки (.JPEG,
                                .PNG),<br />— видеоролики (MP4, AVI, MOV),<br
                                />— документы (.DOCX, .DOC, .ODT, .PDF),<br />—
                                таблицы (.XLS, .XLSX)</Helper
                            >
                            <Listgroup
                                items={strct.files}
                                let:item
                                class="mt-2"
                            >
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
    {/each}
</div>
