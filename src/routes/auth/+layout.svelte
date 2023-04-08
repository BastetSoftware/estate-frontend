<script>
    import "../../app.postcss";
    import "../styles.css";

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
        User,
        ComputerDesktop,
        DocumentText,
        ArrowRightOnRectangle,
        Cog6Tooth,
    } from "@steeze-ui/heroicons";
</script>

<div class="app">
    <main>
        <slot />
    </main>
</div>
