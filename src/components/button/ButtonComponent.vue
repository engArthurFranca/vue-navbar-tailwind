<script setup>
	import { defineProps } from 'vue';

	const props = defineProps({
		liClass: {
			type: String
		},
		divClass: {
			type: String
		}
	});
	
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
</template>