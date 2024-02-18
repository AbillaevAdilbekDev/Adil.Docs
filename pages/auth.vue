<script lang="ts" setup>
import { ACCOUNT } from '~/libs/appwrite'
import { useLoadingStore } from '~/store/loading.store'

definePageMeta({ layout: 'auth' })
useHead({ title: 'Auth | Adil.Docs' })

const router = useRouter()
const loadingStore = useLoadingStore()

onMounted(() => {
	ACCOUNT.get()
		.then(() => router.push('/'))
		.catch(() => loadingStore.set(false))
})

const isLogin = ref(true)

const toggleLogin = () => (isLogin.value = !isLogin.value)

const onGoogle = () =>
	ACCOUNT.createOAuth2Session('google', 'https://jira.sammi.app')

const onGithub = () =>
	ACCOUNT.createOAuth2Session('github', 'https://jira.sammi.app')
</script>

<template>
	<UiLoader v-if="loadingStore.isLoading" />

	<div class="flex items-center justify-center h-screen w-full relative" v-else>
		<NuxtImg
			src="/bg-auth.jpg"
			class="absolute inset-0 w-full h-full object-cover z-10"
		/>
		<div
			class="absolute inset-0 w-full h-full z-20 dark:bg-black/40 bg-white/40"
		></div>
		<UCard class="z-50 w-1/2 relative" :ui="{ body: { base: 'flex gap-4' } }">
			<div class="space-y-4 flex-1">
				<h1 class="text-2xl font-bold">
					<template v-if="isLogin">Dasturge kiriw</template>
					<template v-else>Dizimnen otiw</template>
				</h1>

				<p class="opacity-70">
					<template v-if="isLogin"
						>Iltimas Dasturge kiriw ushin tomendegilerdi toltirin'</template
					>
					<template v-else>
						Dizimnen otiw ushin tomendegilerdi toltirin'
					</template>
				</p>

				<AuthLogin v-if="isLogin" :toggle-login="toggleLogin" />
				<AuthRegister v-else :toggle-login="toggleLogin" />
			</div>
			<UDivider label="Yamasa" orientation="vertical" class="w-fit" />
			<div class="space-y-4 flex flex-1 flex-col justify-center">
				<UButton color="black" block size="lg" @click="onGithub">
					<Icon name="mdi:github" class="w-5 h-5" />
					<span>GitHub arqali dizimnen otiw</span>
				</UButton>
				<UButton color="black" block size="lg" @click="onGoogle">
					<Icon name="ri:google-fill" class="w-5 h-5" />
					<span>Google arqali dizimnen otiw</span>
				</UButton>
			</div>
		</UCard>
	</div>
</template>
