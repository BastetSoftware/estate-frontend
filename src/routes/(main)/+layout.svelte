<script>
    import "../../app.postcss";
    import "../../styles.css";

    import {
        Navbar,
        NavBrand,
        NavLi,
        NavUl,
        NavHamburger,
        Card,
        Button,
        Avatar,
        Dropdown,
        DropdownItem,
        DropdownDivider,
        DropdownHeader,
        Activity,
        ActivityItem,
        Pagination,
        PaginationItem,
        SpeedDial,
        SpeedDialButton,
    } from "flowbite-svelte";

    import { Icon } from "@steeze-ui/svelte-icon";

    import {
        ArrowRight,
        HomeModern,
        QuestionMarkCircle,
        Users,
        User,
        ComputerDesktop,
        DocumentText,
        ArrowRightOnRectangle,
        Cog6Tooth,
        Plus,
        DocumentCheck,
    } from "@steeze-ui/heroicons";
</script>

<div class="app">
    <main>
        <Navbar
            let:hidden
            let:toggle
            navClass="w-full sticky top-0 z-20"
            navDivClass="w-full flex flex-col justify-between pt-2 md:pt-0 pb-0 pl-4 pr-4 items-center max-w-full"
        >
            <div
                class="w-full flex flex-row justify-between items-center max-w-full"
            >
                <NavBrand href="/">
                    <img alt="" class="w-12 h-12" src="/logo.svg" />
                </NavBrand>
                <div class="flex flex-row gap-4">
                    <NavUl>
                        <NavLi href="/" class="flex items-center min-w-fit"
                            ><Icon src={ComputerDesktop} class="w-6 pr-2 p-0" />
                            Главная</NavLi
                        >
                        <NavLi
                            href="/object/list"
                            class="flex items-center min-w-fit"
                            ><Icon src={HomeModern} class="w-6 pr-2 p-0" /> Объекты</NavLi
                        >
                        <NavLi
                            href="/task/list"
                            class="flex items-center min-w-fit"
                            ><Icon src={DocumentText} class="w-6 pr-2 p-0" /> Задачи</NavLi
                        >
                        <NavLi
                            href="/report/list"
                            class="flex items-center min-w-fit"
                            ><Icon src={DocumentCheck} class="w-6 pr-2 p-0" /> Отчёты</NavLi
                        >
                        <NavLi
                            href="/account/list"
                            class="flex items-center min-w-fit"
                            ><Icon src={Users} class="w-6 pr-2 p-0" /> Люди</NavLi
                        >
                        <NavLi href="/help" class="flex items-center min-w-fit"
                            ><Icon
                                src={QuestionMarkCircle}
                                class="w-6 pr-2 p-0"
                            /> Справка</NavLi
                        >
                    </NavUl>
                    <div class="flex items-center md:order-2 place-self-right">
                        <Avatar id="avatar-menu" />
                        <NavHamburger
                            on:click={toggle}
                            class1="w-full md:flex md:w-auto md:order-1"
                        />
                    </div>
                    <Dropdown placement="bottom" triggeredBy="#avatar-menu">
                        <DropdownHeader>
                            <b
                                ><span class="block text-sm">Никитин И. С.</span
                                ></b
                            >
                        </DropdownHeader>
                        <DropdownItem
                            class="flex items-center flex-row gap-x-2"
                            href="/account/"
                            ><Icon src={User} class="w-6" /> Профиль</DropdownItem
                        >
                        <DropdownItem
                            class="flex items-center flex-row gap-x-2"
                            href="/account/settings"
                            ><Icon src={Cog6Tooth} class="w-6" /> Настройки</DropdownItem
                        >
                        <DropdownDivider />
                        <DropdownItem class="flex items-center flex-row gap-x-2"
                            ><Icon src={ArrowRightOnRectangle} class="w-6" /> Выйти</DropdownItem
                        >
                    </Dropdown>
                </div>
            </div>
            <div class="md:hidden w-full p-0 m-0 py-1">
                <NavUl {hidden} ulClass="flex flex-col">
                    <NavLi href="/" class="flex items-center min-w-fit"
                        ><Icon src={ComputerDesktop} class="w-6 pr-2 p-0" /> Главная</NavLi
                    >
                    <NavLi
                        href="/object/list"
                        class="flex items-center min-w-fit"
                        ><Icon src={HomeModern} class="w-6 pr-2 p-0" /> Объекты</NavLi
                    >
                    <NavLi href="/task/list" class="flex items-center min-w-fit"
                        ><Icon src={DocumentText} class="w-6 pr-2 p-0" /> Задачи</NavLi
                    >
                    <NavLi
                        href="/report/list"
                        class="flex items-center min-w-fit"
                        ><Icon src={DocumentCheck} class="w-6 pr-2 p-0" /> Отчёты</NavLi
                    >
                    <NavLi
                        href="/account/list"
                        class="flex items-center min-w-fit"
                        ><Icon src={Users} class="w-6 pr-2 p-0" /> Люди</NavLi
                    >
                    <NavLi href="/help" class="flex items-center min-w-fit"
                        ><Icon src={QuestionMarkCircle} class="w-6 pr-2 p-0" /> Справка</NavLi
                    >
                </NavUl>
            </div>
        </Navbar>
        <div class="flex justify-center w-full">
            <div class="w-full xl:w-5/6">
                <slot />
            </div>
        </div>
        <SpeedDial defaultClass="fixed right-6 bottom-6">
            <Icon slot="icon" src={Plus} class="w-6" />
            <SpeedDialButton name="Новый объект..." href="/object/new">
                <Icon src={HomeModern} class="w-6 h-6" theme="solid" />
            </SpeedDialButton>
            <SpeedDialButton name="Новая задача..." href="/task/new">
                <Icon src={DocumentText} class="w-6 h-6" theme="solid" />
            </SpeedDialButton>
            <SpeedDialButton name="Новый отчёт..." href="/task/new">
                <Icon src={DocumentCheck} class="w-6 h-6" theme="solid" />
            </SpeedDialButton>
        </SpeedDial>
    </main>
</div>
