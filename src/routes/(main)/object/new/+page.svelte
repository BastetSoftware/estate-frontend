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
        Helper,
        Textarea,
    } from "flowbite-svelte";

    import { Icon } from "@steeze-ui/svelte-icon";
    import {
        Folder,
        DocumentArrowUp,
        DocumentText,
    } from "@steeze-ui/heroicons";
    import { Telegram, Discord, Whatsapp } from "@steeze-ui/simple-icons";

    let images = [];
    let showThumbs = false;

    let countries = [
        { value: "us", name: "United States" },
        { value: "ca", name: "Canada" },
        { value: "fr", name: "France" },
    ];

    let files;
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

    import { SendAPICall } from "$lib/API.svelte";
    import { goto } from "$app/navigation";
    import { get } from "svelte/store";
    import { storage } from "$lib/Storage";

    async function SubmitObject() {
        var data = await SendAPICall("object_create", {
            Token: get(storage).token,
            Name: name.toString(),
            Description: desc.toString(),
            District: district.toString(),
            Region: region.toString(),
            Address: address.toString(),
            Area: parseInt(area.toString()),
            Type: type.toString(),
            State: state.toString(),
            Owner: owner.toString(),
            Actual_user: actual_user.toString(),
            Gid: 2,
            Permissions: 255
        });

        if (data.Code) {
            alert(`Произошла ошибка (${data.Code}).`);
            return;
        }

        alert("Данные успешно обновились!");
        goto(`/object/${data.Id}`);
    }

    const submitBtn = async () => {
        await SubmitObject();
    };
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
                <Button class="bg-gray-500 w-full"
                    >Заполнить из .XML-файла <Icon
                        src={DocumentText}
                        class="w-4 ml-1 p-0"
                    /></Button
                >
                <div
                    class="grid grid-cols-1 lg:grid-cols-2 pt-3 gap-x-3 gap-y-3 text-zinc-800"
                >
                    <Input
                        placeholder="Название"
                        id="name"
                        defaultClass="lg:col-span-2"
                        name="name"
                        type="text"
                        bind:value={name}
                    />
                    <div class="flex flex-col gap-y-3">
                        <Input
                            placeholder="Адрес"
                            id="address"
                            name="floating_outlined"
                            type="text"
                            bind:value={address}
                        />
                        <Select
                            placeholder="Регион"
                            items={countries}
                            bind:value={region}
                        />
                        <Select
                            placeholder="Округ"
                            items={countries}
                            bind:value={district}
                        />
                        <Select
                            placeholder="Тип объекта"
                            items={countries}
                            bind:value={type}
                        />
                    </div>
                    <div class="flex flex-col gap-y-3">
                        <Input
                            placeholder="Площадь (м²)"
                            id="area"
                            name="floating_outlined"
                            type="number"
                            bind:value={area}
                        />
                        <Input
                            placeholder="Состояние"
                            id="state"
                            name="floating_outlined"
                            type="text"
                            bind:value={state}
                        />
                        <Input
                            placeholder="Собственник"
                            id="owner"
                            name="floating_outlined"
                            type="text"
                            bind:value={owner}
                        />
                        <Input
                            placeholder="Фактический пользователь"
                            id="actual_user"
                            name="floating_outlined"
                            type="text"
                            bind:value={actual_user}
                        />
                    </div>
                    <Textarea
                        id="desc"
                        placeholder="Описание"
                        bind:value={desc}
                        class="lg:col-span-2"
                    />
                    <Button on:click={submitBtn} class="lg:col-span-2"
                        >Внести в базу <Icon
                            src={DocumentArrowUp}
                            class="w-4 ml-1 p-0"
                        /></Button
                    >
                </div>
            </form>
        </Card>
    </div>
    <div class="w-full lg:w-1/2 flex flex-col gap-y-3 h-min">
        <Card class="flex grow h-min min-w-full">
            <form>
                <div class="grid grid-cols-1 gap-x-3 gap-y-3 text-zinc-800">
                    <div class="flex flex-col gap-y-3">
                        <h4>Прикрепление файлов</h4>
                        <Fileupload id="multiple_files" multiple bind:files />
                        <Helper
                            >Что поддерживается:<br />— картинки (.JPEG, .PNG),<br
                            />— видеоролики (MP4, AVI, MOV),<br />— документы
                            (.DOCX, .DOC, .ODT, .PDF),<br />— таблицы (.XLS,
                            .XLSX)</Helper
                        >
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
