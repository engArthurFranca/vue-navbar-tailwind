<script setup>
	import { defineProps, toRefs } from 'vue';

	const props = defineProps({
		menuElements: {
			type: Array,
			required: true
		},
		classLight: {
			type: String
		},
		classDark: {
			type: String
		}
	}); 

	const { menuElements, classLight, classDark } = toRefs(props);

	function addDarkPrefix(string) {
    // Divide a string em palavras separadas por espaço
		const words = string.split(' ');
    // Mapeia cada palavra e adiciona o prefixo 'dark:' na frente
		const wordsWithPrefix = words.map(words => 'dark:' + words);
    // Junta as palavras de volta em uma única string
		const newString = wordsWithPrefix.join(' ');
		return newString;
	}
	
</script>

<style scoped>
	.submenu:hover > .hidden {
		display: block;
	}
	.submenu:not(:hover) > .hidden {
		display: none;
	}
</style>

<template>
	<nav :class="classLight + ' ' + addDarkPrefix(classDark)">
		<ul class="flex p-2">
			<li class="relative submenu m-2" v-for="menuItem in menuElements" :key="menuItem.name">
				<!-- Check if there is any submenu -->
				<template v-if="menuItem.submenu">
					<span class="cursor-pointer">{{ menuItem.name }}</span>
					<div class="hidden absolute top-full left-1/2 -translate-x-1/2 w-auto ">
						<li v-for="submenuItem in menuItem.submenu" :key="submenuItem.name" class="m-2">
							<router-link :to="submenuItem.path">{{ submenuItem.name }}</router-link>
						</li>
					</div>
				</template>
				<!-- General Case -->
				<template v-else>
					<router-link :to="menuItem.path">{{ menuItem.name }}</router-link>
				</template>
			</li>
		</ul>
	</nav>
</template>