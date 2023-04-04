<script>
  import "../app.postcss";
  import "./styles.css";

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
  } from "flowbite-svelte";

  import { Icon } from "@steeze-ui/svelte-icon";

  import {
    ArrowRight,
    HomeModern,
    QuestionMarkCircle,
    Users,
    ComputerDesktop,
    DocumentText,
  } from "@steeze-ui/heroicons";
</script>

<div class="app">
  <main>
    <!--<Navbar
      let:hidden
      let:toggle
      navDivClass="mx-auto w-full block flex justify-between"
    >
      <div>
        <NavBrand href="/">
          <img
            src="https://flowbite.com/docs/images/logo.svg"
            class="mr-3 h-6 sm:h-9"
            alt="Flowbite Logo"
          />
          <span
            class="self-center whitespace-nowrap text-xl font-semibold dark:text-white"
            >Bastet System</span
          >
        </NavBrand>
      </div>
      <div class="flex">
        <NavUl
          {hidden}
          divClass="w-full md:block md:w-auto flex place-self-center"
        >
          <NavLi href="/" active={true} class="flex min-w-fit"
            ><Icon src={ComputerDesktop} class="w-6 pr-2 p-0" />Главная</NavLi
          >
          <NavLi href="/" class="flex items-center min-w-fit"
            ><Icon src={HomeModern} class="w-6 pr-2 p-0" /> Объекты</NavLi
          >
          <NavLi href="/about" class="flex items-center min-w-fit"
            ><Icon src={DocumentText} class="w-6 pr-2 p-0" /> Задачи</NavLi
          >
          <NavLi href="/services" class="flex items-center min-w-fit"
            ><Icon src={Users} class="w-6 pr-2 p-0" /> Люди</NavLi
          >
          <NavLi href="/contact" class="flex items-center min-w-fit"
            ><Icon src={QuestionMarkCircle} class="w-6 pr-2 p-0" /> Справка</NavLi
          >
        </NavUl>
        <div class="flex items-center md:order-2 place-self-right">
          <Avatar id="avatar-menu" src="/images/profile-picture-3.webp" />
          <NavHamburger
            on:click={toggle}
            class1="w-full md:flex md:w-auto md:order-1"
          />
        </div>
      </div>
      <Dropdown placement="bottom" triggeredBy="#avatar-menu">
        <DropdownHeader>
          <span class="block text-sm"> Bonnie Green </span>
          <span class="block truncate text-sm font-medium">
            name@flowbite.com
          </span>
        </DropdownHeader>
        <DropdownItem>Dashboard</DropdownItem>
        <DropdownItem>Settings</DropdownItem>
        <DropdownItem>Earnings</DropdownItem>
        <DropdownDivider />
        <DropdownItem>Sign out</DropdownItem>
      </Dropdown>
    </Navbar>-->
    <slot />
  </main>
</div>
