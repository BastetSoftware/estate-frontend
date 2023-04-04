<script>
    import {
        Avatar,
        Card,
        Label,
        Input,
        Checkbox,
        Button,
        FloatingLabelInput
    } from "flowbite-svelte";

    import { Icon } from "@steeze-ui/svelte-icon";

    import { DocumentArrowUp } from "@steeze-ui/heroicons";
</script>

<svelte:head>
    <title>Home</title>
    <meta name="description" content="Svelte demo app" />
</svelte:head>

<div class="w-full p-5 pb-3">
    <h1 class="ml-0 mr-3">Аккаунт</h1>
    <p class="m-0 p-0 text-gray-400">
        настройки системы, изменение личной информации
    </p>
</div>
<div class="p-5 w-full grid lg:grid-cols-3 grid-cols-1 gap-x-3 gap-y-3">
    <Card horizontal class="grow shrink h-min text-zinc-800 min-w-full">
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
    <Card class="flex grow h-min min-w-full col-span-2">
        <h2 class="text-zinc-800">Информация</h2>
        <form>
            <div
                class="grid grid-cols-1 lg:grid-cols-2 pt-3 gap-x-3 gap-y-3 text-zinc-800 mb-3"
            >
                <div>
                    <FloatingLabelInput style="outlined" id="surname" name="floating_outlined" type="text" label="Фамилия" class="mb-3" value="Никитин"/>
                    <FloatingLabelInput style="outlined" id="name" name="floating_outlined" type="text" label="Имя" class="mb-3" value="Иван"/>
                    <FloatingLabelInput style="outlined" id="patronymic" name="floating_outlined" type="text" label="Отчество" class="mb-3" value="Сергеевич" />
                </div>
                <div>
                    <FloatingLabelInput style="outlined" id="email" name="email" type="email" label="Основной адрес эл. почты" class="mb-3" value="nikitin_ivan@example.com"/>
                    <Checkbox class="mb-2">Получать оповещения</Checkbox>
                    <Checkbox checked class="mb-2"
                        >Сделать почту публичной</Checkbox
                    >
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
    <Card class="flex grow h-min min-w-full lg:col-span-2 lg:col-start-2">
        <h2 class="text-zinc-800">Безопасность</h2>
        <form>
            <div
                class="grid grid-cols-1 lg:grid-cols-2 pt-3 gap-x-3 gap-y-3 text-zinc-800 mb-3"
            >
                <div>
                    <p class="mb-1"><b>Смена пароля</b></p>
                    <FloatingLabelInput style="outlined" id="password" name="password" type="password" label="Новый пароль" class="mb-3"/>
                    <FloatingLabelInput style="outlined" id="old_password" name="old_password" type="password" label="Старый пароль" class="mb-3"/>
                </div>
                <div>
                    
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
