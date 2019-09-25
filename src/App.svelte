<script>
let promise = getUser()

async function getUser() {
		const res = await fetch(`https://randomuser.me/api/?male=female?results=1`);
		const data = await res.text();

		if (res.ok) {
			let json = JSON.parse(data)
			return json.results[0];

		} else {
			throw new Error(res);
		}
	}

</script>
<svelte:head>
	<title>Svelte + Tailwind CSS</title>
</svelte:head>
<div>
{#await promise then value}
<div class="border-solid border-2 sm:border-dashed md:border-dotted lg:border-double xl:border-none bg-blue-100 rounded-lg p-6 md:w-5/12 shadow-xl xs:w-full ">
	<img class="h-16 w-16 rounded-full mx-auto" src="{value.picture.thumbnail}" alt='User Photo'>
	<div class="text-center">
		<h2 class="text-lg">{value.name.first} {value.name.last} </h2>
		<div class="text-purple-500">{value.login.username.toUpperCase()}</div>
		<div class="text-gray-600">{value.email} </div>
		<div class="text-gray-600">{value.phone}</div>
	</div>
</div>
{/await}
</div>