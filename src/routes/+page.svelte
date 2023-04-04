<script>
	import {
		Card,
		Button,
		Activity,
		ActivityItem,
		PaginationItem,
	} from "flowbite-svelte";

	import { Icon } from "@steeze-ui/svelte-icon";

	import {
		ArrowRight,
	} from "@steeze-ui/heroicons";

	let activities = [
		{
			title: '<span class="text-blue-500 font-bold">Петров П. Ю.</span> отправил отчёт по задаче <span class="text-blue-500 font-bold">#311 Список материалов для реставрации</span>.',
			date: "минуту назад",
			src: "/images/profile-picture-2.webp",
			alt: ""
		},
		{
			title: '<span class="text-blue-500 font-bold">Иванов Г. С.</span> внёс в систему новый объект: <span class="text-blue-500 font-bold"> 3-й Сетуньский проезд, 8, Москва, 119136</span>.',
			date: "четыре минуты назад",
			src: "/images/profile-picture-2.webp",
			text: "Описание: ...",
			alt: ""
		},
		{
			title: '<span class="text-blue-500 font-bold">Сидорова М. А.</span> изменила статус задачи <span class="text-blue-500 font-bold">#311 Список материалов для реставрации</span>.',
			date: "два часа назад",
			src: "/images/profile-picture-3.webp",
			alt: ""
		},
	];

	const previous = () => {
    alert('Previous btn clicked. Make a call to your server to fetch data.');
  };
  const next = () => {
    alert('Next btn clicked. Make a call to your server to fetch data.');
  };
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<div class="w-full p-5 pb-3 ">
    <h1 class="ml-0 mr-3">Главная</h1> <p class="m-0 p-0 text-gray-400">панель управления, просмотр последних событий</p>
</div>
<div class="grid grid-cols-1 lg:grid-cols-2 gap-x-3 gap-y-3">
	<div class="w-full pt-0 pl-5">
		<h3 class="mb-3">Лента событий</h3>
		<Activity olClass="w-full ml-3 mb-0 pb-0 relative">
			<ActivityItem {activities} />
		</Activity>
		<div class="w-full flex space-x-3 justify-center">
			<PaginationItem on:click={previous}>Назад</PaginationItem>
  			<PaginationItem on:click={next}>Дальше</PaginationItem>
		</div>
	</div>
	<div class="w-full pr-3 pt-0 mt-0">
		<h3 class="ml-0 ml-3 mb-3">Быстрый доступ</h3>
		<div class="grid grid-cols-1 lg:grid-cols-2 gap-3 p-3 pt-0">
			<Card class="grow shrink h-min min-w-full">
				<div class="mb-1 text-zinc-800">
					<h3>Объекты</h3>
					<p class="mt-1">Работы ведутся на 17 площадках</p>
				</div>

				<Button class="w-fit">
					Просмотреть <Icon
						src={ArrowRight}
						class="w-4 ml-1 p-0"
					/>
				</Button>
			</Card>
			<Card class="grow shrink h-min min-w-full">
				<div class="mb-1 text-zinc-800">
					<h3>Отчёты</h3>
					<p class="mt-1">Новых отчётов ещё нет</p>
				</div>

				<Button class="w-fit">
					Открыть <Icon
						src={ArrowRight}
						class="w-4 ml-1 p-0"
					/>
				</Button>
			</Card>
			<Card class="grow shrink h-min min-w-full">
				<div class="mb-1 text-zinc-800">
					<h3>Задачи</h3>
					<p class="mt-1">12 задач изменили статус</p>
				</div>

				<Button class="w-fit">
					Проверить <Icon
						src={ArrowRight}
						class="w-4 ml-1 p-0"
					/>
				</Button>
			</Card>
			<Card class="grow shrink h-min min-w-full">
				<div class="mb-1 text-zinc-800">
					<h3>Люди</h3>
					<p class="mt-1">Свяжитесь с нужными людьми</p>
				</div>

				<Button class="w-fit">
					Просмотреть <Icon
						src={ArrowRight}
						class="w-4 ml-1 p-0"
					/>
				</Button>
			</Card>
		</div>
	</div>
</div>
