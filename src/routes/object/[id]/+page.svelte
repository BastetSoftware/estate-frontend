<script>
    import {
        Avatar,
        Card,
        Carousel,
        CarouselTransition,
    } from "flowbite-svelte";

    import { Icon } from "@steeze-ui/svelte-icon";
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
</script>

<svelte:head>
    <title>Home</title>
    <meta name="description" content="Svelte demo app" />
</svelte:head>

<div class="w-full p-5 pb-0">
    <h1 class="ml-0 mr-3">Объект</h1>
    <p class="m-0 p-0 text-gray-400">просмотр сведений об объекте</p>
</div>
<div class="p-5 w-full flex flex-col lg:flex-row gap-x-3 gap-y-3">
    <div class="w-full lg:w-1/2">
        <Card class="h-min text-zinc-800 min-w-full">
            <div class="text-zinc-800">
                <h4>3-й Сетуньский проезд, 8, Москва, 119136</h4>
            </div>
            <Carousel {images} {showThumbs} />
        </Card>
    </div>
    <div class="w-full lg:w-1/2 flex flex-col gap-y-3 h-min">
        <Card class="flex grow h-min min-w-full">
            <div class="grid grid-cols-1 gap-x-3 gap-y-3 text-zinc-800">
                <div class="flex flex-col gap-y-3">
                    <h4>Общая информация</h4>
                </div>
                <div class="flex flex-col gap-y-3">
                    <div>
                        <b>Адрес</b>
                        <p>3-й Сетуньский проезд, 8, Москва, 119136</p>
                    </div>
                    <div>
                        <b>Координаты</b>
                        <p><a href="geo:55.732945,37.535763">55.732945, 37.535763</a></p>
                    </div>
                    <!--<div class="flex flex-row gap-x-3 gap-y-1">
                    </div>-->
                </div>
            </div>
        </Card>
    </div>
</div>
