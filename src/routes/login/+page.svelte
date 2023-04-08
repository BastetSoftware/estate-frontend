
<script>
import { Button, Dropdown, DropdownItem, Chevron } from 'flowbite-svelte'
import { Navbar, NavBrand, NavLi, NavUl, NavHamburger } from 'flowbite-svelte'
import { BottomNav, BottomNavItem } from "flowbite-svelte"
</script>

<Navbar let:hidden let:toggle>
    <NavBrand>
      <img
        src="https://www.alumnirussia.org/ckfinder/userfiles/images/raof/MIREA_Gerb_Colour.jpg"
        class="mr-3 h-6 sm:h-9"
        alt="MIREA Logo"
      />
      <span class="text-blue-500 uppercase self-center whitespace-nowrap text-xl font-semibold dark:text-white overline">
          Bastet Software
      </span>
    </NavBrand>
  </Navbar>


<style>
body {
    background-color: #F9FAFB;
}

form {
    background-color: #ffffff;
    width: 500px;
    text-transform: uppercase;
    border-radius: 15px;
    box-shadow: 0 0 5px rgba(122,122,122,0.5);
}

h1 {
    background-color: #ffffff;
    width: 500px;
    padding-bottom: 5px;
    border-bottom: 3px solid #4382ff;
    width: 500px;
    margin: 10px;
    border-radius: 15px;
    box-shadow: 0 0 5px rgba(122,122,122,0.5);
}

input {
    margin-bottom: 10px;
    margin-top: 3px;
    background-color: #F9FAFB;
    border-radius: 5px;
    border-bottom: 3px solid #F9FAFB;
    border-left: 3px solid #F9FAFB;
    border-right: 3px solid #F9FAFB;
    border-top: 3px solid #F9FAFB;
    width: 300px;
}

</style>

<body>
<center>
<h1 style="color:#17202A" class="uppercase">Регистрация</h1>

        <form>
            <p style="color:#17202A">
                <label for="login">Логин:</label>
                <p>
                    <input type="text" placeholder="Введите логин" class="login">
                </p>

            <p style="color:#17202A">
                <label for="login">Пароль:</label>
                <p>
                    <input type="text" placeholder="Введите пароль" class="pass">
                </p>

            <p style="color:v#17202A">
                <label for="login">Повторите пароль:</label>
                <p>
                    <input type="text" placeholder="Введите пароль" class="passom">
                </p>

            <p style="color:#17202A">
                <label for="login">Адрес электронной почты:</label>
                <p>
                    <input type="text" placeholder="Введите адрес электронной почты" class="email">
                </p>
                <button type="button" class="text-white uppercase bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 mr-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 focus:outline-none dark:focus:ring-blue-800">Зарегистрироваться</button>

            <p>

        </form>
</center>
</body>