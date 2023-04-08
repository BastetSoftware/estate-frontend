<script>
    import { storage } from "$lib/Storage";

    import { Button, Dropdown, DropdownItem, Chevron } from "flowbite-svelte";
    import {
        Navbar,
        NavBrand,
        NavLi,
        NavUl,
        NavHamburger,
    } from "flowbite-svelte";
    import { BottomNav, BottomNavItem } from "flowbite-svelte";

    import { SendAPICall } from "$lib/API.svelte";
    import { goto } from "$app/navigation";
    import { get } from 'svelte/store'

    let loginInput = "";
    let pwdInput = "";

    async function Login() {
        var data = await SendAPICall("user_log_in", {
            Login: loginInput.toString(),
            Password: pwdInput.toString(),
        });

        if (data.Code) {
            alert(
                `Произошла ошибка входа (${data.Code}). Проверьте правильность учётных данных.`
            );
            return;
        }

        var accountData = await SendAPICall("user_get_info", {
            Login: loginInput.toString(),
            Token: data.Token
        });
        
        let whoami = `${accountData.LastName} ${accountData.FirstName[0]}.`;
        if (accountData.Patronymic != "-") {
            whoami += ' ' + accountData.Patronymic[0] + '.';
        }
        
        storage.set({ token: data.Token, login: loginInput.toString(), whoami: whoami });
        goto("/");
    }

    const loginBtn = async () => {
        await Login();
    };
</script>

<body>
    <center>
        <h1 style="color:#17202A text-xl">Войти в аккаунт</h1>

        <form>
            <p style="color:#17202A">
                <label for="username">Логин:</label>
            </p>
            <p>
                <input
                    type="text"
                    name="username"
                    placeholder="Введите логин"
                    class="pass"
                    bind:value={loginInput}
                />
            </p>

            <p style="color:#17202A">
                <label for="login">Пароль:</label>
            </p>
            <p>
                <input
                    type="password"
                    placeholder="Введите пароль"
                    class="pass"
                    bind:value={pwdInput}
                />
            </p>
            <button
                type="button"
                on:click={loginBtn}
                class="text-white uppercase bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800"
                >Войти</button
            >
            <p />
            <p>Или</p>
            <button
                type="button"
                class="text-white uppercase bg-gray-400 hover:bg-gray-500 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800"
                >Зарегистрироваться</button
            >
            <p />
        </form>
    </center>
</body>

<style>
    body {
        background-color: #f9fafb;
        margin: 0;
        padding: 0;
    }

    form {
        background-color: #ffffff;
        width: 500px;
        text-transform: uppercase;
        border-radius: 15px;
        box-shadow: 0 0 5px rgba(122, 122, 122, 0.5);
    }

    h1 {
        background-color: #ffffff;
        width: 500px;
        margin-bottom: 5px;
        border-bottom: 3px solid #4382ff;
        margin: 10px;
        border-radius: 15px;
        box-shadow: 0 0 5px rgba(122, 122, 122, 0.5);
    }

    input {
        margin-bottom: 10px;
        margin-top: 3px;
        background-color: #f9fafb;
        border-radius: 5px;
        border-bottom: 3px solid #f9fafb;
        border-left: 3px solid #f9fafb;
        border-right: 3px solid #f9fafb;
        border-top: 3px solid #f9fafb;
        width: 300px;
    }
</style>
