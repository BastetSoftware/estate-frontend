<script>
    import {
        Avatar,
        Card,
        Checkbox,
        Button,
        FloatingLabelInput,
    } from "flowbite-svelte";

    import { Icon } from "@steeze-ui/svelte-icon";
    import { DocumentArrowUp, PlusCircle, Trash } from "@steeze-ui/heroicons";
</script>

<svelte:head>
    <title>Home</title>
    <meta name="description" content="Svelte demo app" />
</svelte:head>

<div class="w-full p-5 pb-0">
    <h1 class="ml-0 mr-3">Настройки</h1>
    <p class="m-0 p-0 text-gray-400">
        управление системой, изменение личной информации
    </p>
</div>
<div class="p-5 w-full flex flex-col lg:flex-row gap-x-3 gap-y-3">
    <div class="w-full lg:w-1/3">
        <Card horizontal class="h-min text-zinc-800 min-w-full text-center">
            <div
                class="flex wrap items-center justify-center flex-col grow text-zinc-800"
            >
                <Avatar size="xl" class="mr-3 mb-3" />
                <h2>Никитин Иван Сергеевич</h2>
                <p>системный администратор</p>
                <p>логин:</p>
                <pre>nikitin_ivan</pre>
            </div>
        </Card>
    </div>
    <div class="w-full lg:w-2/3 flex flex-col gap-y-3 h-min">
        <Card class="flex grow h-min min-w-full">
            <h2 class="text-zinc-800">Общая информация</h2>
            <form>
                <div
                    class="grid grid-cols-1 lg:grid-cols-2 pt-3 gap-x-3 gap-y-3 text-zinc-800 mb-3"
                >
                    <div class="flex flex-col gap-y-3">
                        <FloatingLabelInput
                            style="outlined"
                            id="surname"
                            name="floating_outlined"
                            type="text"
                            label="Фамилия"
                            value="Никитин"
                        />
                        <FloatingLabelInput
                            style="outlined"
                            id="name"
                            name="floating_outlined"
                            type="text"
                            label="Имя"
                            value="Иван"
                        />
                        <FloatingLabelInput
                            style="outlined"
                            id="patronymic"
                            name="floating_outlined"
                            type="text"
                            label="Отчество"
                            value="Сергеевич"
                        />
                    </div>
                    <div class="flex flex-col gap-y-3">
                        <FloatingLabelInput
                            style="outlined"
                            id="email"
                            name="email"
                            type="email"
                            label="Основной адрес эл. почты"
                            value="nikitin_ivan@example.com"
                        />
                        <Checkbox>Получать оповещения</Checkbox>
                        <Checkbox checked>Использовать для подтверждения входа</Checkbox>
                    </div>
                </div>
            </form>
            <Button
                >Сохранить <Icon
                    src={DocumentArrowUp}
                    class="w-4 ml-1 p-0"
                /></Button
            >
        </Card>
        <Card class="flex grow h-min min-w-full">
            <h2 class="text-zinc-800">Безопасность</h2>
            <form>
                <div
                    class="grid grid-cols-1 lg:grid-cols-2 pt-3 gap-x-3 gap-y-3 text-zinc-800 mb-3"
                >
                    <div class="lg:col-span-2"><b>Смена пароля</b></div>
                    <div class="flex flex-col gap-y-3">
                        <FloatingLabelInput
                            style="outlined"
                            id="password"
                            name="password"
                            type="password"
                            label="Новый пароль"
                        />
                    </div>
                    <div class="flex flex-col gap-y-3">
                        <FloatingLabelInput
                            style="outlined"
                            id="old_password"
                            name="old_password"
                            type="password"
                            label="Старый пароль"
                        />
                    </div>
                </div>
            </form>
            <Button
                >Сохранить <Icon
                    src={DocumentArrowUp}
                    class="w-4 ml-1 p-0"
                /></Button
            >
        </Card>
        <Card class="flex grow h-min min-w-full">
            <h2 class="text-zinc-800">Контакты</h2>
            <form>
                <div
                    class="grid grid-cols-1 lg:grid-cols-2 pt-3 gap-x-3 gap-y-3 text-zinc-800 mb-3"
                >
                    <p class="lg:col-span-2"><b>Адреса эл. почты</b></p>
                    <div class="flex flex-col gap-y-3">
                        <div class="flex flex-row gap-x-3 w-full">
                            <div class="w-full">
                                <FloatingLabelInput
                                    style="outlined"
                                    id="email1"
                                    name="email1"
                                    type="email"
                                    label="Адрес 1"
                                />
                            </div>
                            <Button color="red">
                                <Icon src={Trash} class="w-4" />
                            </Button>
                        </div>
                        <div class="flex flex-row gap-x-3 w-full">
                            <div class="w-full">
                                <FloatingLabelInput
                                    style="outlined"
                                    id="email2"
                                    name="email2"
                                    type="email"
                                    label="Адрес 2"
                                />
                            </div>
                            <Button color="red">
                                <Icon src={Trash} class="w-4" />
                            </Button>
                        </div>
                        <Button>
                            Добавить<Icon
                                src={PlusCircle}
                                class="w-4 ml-1 p-0"
                            />
                        </Button>
                    </div>
                    <div class="flex flex-col gap-y-3">
                        <FloatingLabelInput
                            style="outlined"
                            id="old_password"
                            name="old_password"
                            type="password"
                            label="Старый пароль"
                        />
                    </div>
                </div>
            </form>
            <Button
                >Сохранить <Icon
                    src={DocumentArrowUp}
                    class="w-4 ml-1 p-0"
                /></Button
            >
        </Card>
    </div>
</div>
