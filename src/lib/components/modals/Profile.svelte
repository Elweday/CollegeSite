<script>
	// @ts-nocheck
	import { Avatar } from "@skeletonlabs/skeleton";
	import { myCustomTheme } from "$lib/../theme.js";
	import { goto } from '$app/navigation';
	import {Color}  from "$lib/utils/colors.js";
	import {  setContext } from "svelte";
	let stats = [
		{ title: "CGPA", value: "3.56", outof: "4.00" },
	];
	function logout(e) {
		fetch("/api/auth/logout", { method: "POST" });
		goto('/login');
		
	}
	
	let theme = "the-theme"
	function changeTheme() {
		let body = document.querySelector('body')
		body.setAttribute("data-theme", theme);
		const styles = getComputedStyle(body);
		const primaryColor = styles.getPropertyValue("--color-primary-500")
		localStorage.setItem("theme", theme)
		console.log(primaryColor)
		setContext('color', new Color(...primaryColor.split(" ")))
	}

	
</script>

<section class="card h-[40rem] w-80 flex p-5  flex-col">
	<div class="flex items-center justify-between">
		<span class="text-gray-400 text-sm">Profile Settings</span>
		<span class="text-primary-400">
			<svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
				<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 12h.01M12 12h.01M19 12h.01M6 12a1 1 0 11-2 0 1 1 0 012 0zm7 0a1 1 0 11-2 0 1 1 0 012 0zm7 0a1 1 0 11-2 0 1 1 0 012 0z" />
			</svg>
		</span>
	</div>
	<div class="mt-6 w-fit mx-auto">
		<Avatar src="/OIP.jpg" width="w-32" rounded="rounded-full" border="border-2" />
	</div>

	<h2 class="text-white font-bold text-lg tracking-wide text-center mt-2">Mohammed Nasser Hilal Ahmed</h2>

	<p class="text-primary-400 font-semibold mt-2">CIE department, Level 3</p>
	<div class="relative flex flex-col gap-4 py-3 h-full">
		{#each stats as { title, value, outof }}
			<div class="flex flex-col items-center gap-0.5 group">
				<span class="w-full text-gray-400 font-semibold text-sm">{title}:</span>
				<div class="h-1 w-full bg-black rounded-full m-0 p-0">
					<div class="h-1 rounded-full w-3/5 bg-yellow-500 fill relative" style={`width: ${(100 * value) / outof}%`}>
						<span class="absolute -top-4 -right-6 text-center text-white shadow-xl p-1 opacity-0 font-extrabold group-hover:opacity-80 transition-opacity duration-300 w-8 rounded-full grid place-content-center aspect-square">{value}</span>
					</div>
				</div>
			</div>
		{/each}
		<div class="flex flex-col items-center gap-0.5 group">
			<span class="w-full text-gray-400 font-semibold text-sm">Preferred Theme:</span>
			<select class="select" bind:value={theme} on:change={changeTheme}>
				{#each ["skeleton", "modern", "crimson", "wintry", "gold-nouveau", "hamlindigo", "rocket", "sahara", "vintage", "seafoam"] as  t}
					<option value={t}>{t}</option>
				{/each}
			</select>
		</div>
		<div class="absolute bottom-4 flex flex-col items-center gap-0.5 group place-self-center">
			<button type="submit" on:click={logout}  class="btn bg-error-500 text-sm ">
				Logout 				
			</button>
		</div>
		

	
	</div>
</section>

<style>
	.fill {
		animation: fill 1s forwards ease-in-out;
		animation-delay: 0.3s;
	}
	@keyframes fill {
		from {
			width: 0%;
		}
	}
</style>
