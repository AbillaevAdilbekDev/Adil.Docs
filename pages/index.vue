<script lang="ts" setup>
import { tabs, templates } from '@/constants'
import { useAuthStore } from '~/store/auth.store'

useHead({ title: 'Adil.Docs' })

const { currentUser } = useAuthStore()
</script>

<template>
	<main class="pb-72">
		<section
			class="flex items-center justify-between h-[100vh] pt-[10vh] gap-4 bg-gradient-to-t from-white dark:from-black to-blue-500 dark:to-blue-800"
		>
			<div class="pl-20 flex flex-col space-y-3">
				<h1 class="text-5xl">
					Omirde o'z maqsetlerin'izdi qolayli qilib qoyin'
				</h1>
				<p class="text-lg opacity-80">
					Omirdi ta'rtipke saliwshi #1 dastur
				</p>
				<template v-if="currentUser.status">
					<NuxtLink to="/documents">
						<UButton color="blue">Maqsetler qoyiw</UButton>
					</NuxtLink>
					<NuxtLink to="https://t.me/adilbekabillaev">
						<UButton color="blue">
							Donat Qiliw
						</UButton>
					</NuxtLink>
				</template>
				<template v-else>
					<NuxtLink to="/auth">
						<UButton color="blue">Biypul Paydalaniw</UButton>
					</NuxtLink>
					<NuxtLink to="https://t.me/adilbekabillaev">
						<UButton color="blue">
							Donat Qiliw
						</UButton>
					</NuxtLink>
				</template>
			</div>
		</section>
	</main>
</template>
