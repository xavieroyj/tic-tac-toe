<script setup lang="ts">
import { createRouter } from 'vue-router'
</script>

<template>
	<main class="container mx-auto px-4 md:px-36 h-screen flex items-center justify-center">
		<div class="flex flex-col items-center gap-4">
			<h1 class="font-bold text-3xl">Tic-Tac-Toe</h1>
			<div>What will you be playing against?</div>
			<RouterLink :to="{ name: 'GameView' }" class="border rounded-md px-4 flex w-full text-xl py-3 justify-center">
				Local
			</RouterLink>
			<button class="border rounded-md px-4 flex w-full text-xl py-3 justify-center">Multiplayer</button>
			<button class="border rounded-md px-4 flex w-full text-xl py-3 justify-center">Machine</button>
		</div>
	</main>
</template>
