<script lang="ts">
	import { BackgroundBeams } from '$lib/components/ui/BackgroundBeams';
	import { BentoGrid, BentoGridItem } from '$lib/components/ui/BentoGrid';
	import HeroParallax from '$lib/components/ui/HeroParallax/HeroParallax.svelte';
	import { ParallaxScroll } from '$lib/components/ui/ParallaxScroll';
	import { ClipboardCopy, File, FileSignature, Table, Waves, Box, Boxes } from 'lucide-svelte';
	import { formSchema, type FormSchema } from './schema';
	import * as Form from "$lib/components/ui/form";
	import { Input } from "$lib/components/ui/input";
	// import { type SuperValidated, type Infer, superForm } from 'sveltekit-superforms';
	// import { zodClient } from 'sveltekit-superforms/adapters';

	// export let data: SuperValidated<Infer<FormSchema>>;

	// const form = superForm(data, {
	// 	validators: zodClient(formSchema)
	// });

	// const { form: formData, enhance } = form;

	let isSkeleton = true;

	const images = [
		'https://images.unsplash.com/photo-1554080353-a576cf803bda?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3387&q=80',
		'https://images.unsplash.com/photo-1505144808419-1957a94ca61e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3070&q=80',
		'https://images.unsplash.com/photo-1470252649378-9c29740c9fa8?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3540&q=80',
		'https://images.unsplash.com/photo-1554080353-a576cf803bda?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3387&q=80',
		'https://images.unsplash.com/photo-1505144808419-1957a94ca61e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3070&q=80',
		'https://images.unsplash.com/photo-1470252649378-9c29740c9fa8?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3540&q=80',
		'https://images.unsplash.com/photo-1682686581854-5e71f58e7e3f?ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3540&q=80',
		'https://images.unsplash.com/photo-1510784722466-f2aa9c52fff6?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3540&q=80',
		'https://images.unsplash.com/photo-1505765050516-f72dcac9c60e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3540&q=80',
		'https://images.unsplash.com/photo-1439853949127-fa647821eba0?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=2640&q=80',
		'https://images.unsplash.com/photo-1554080353-a576cf803bda?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3387&q=80',
		'https://images.unsplash.com/photo-1505144808419-1957a94ca61e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3070&q=80',
		'https://images.unsplash.com/photo-1470252649378-9c29740c9fa8?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3540&q=80',
		'https://images.unsplash.com/photo-1554080353-a576cf803bda?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3387&q=80',
		'https://images.unsplash.com/photo-1505144808419-1957a94ca61e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3070&q=80',
		'https://images.unsplash.com/photo-1554080353-a576cf803bda?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3387&q=80',
		'https://images.unsplash.com/photo-1505144808419-1957a94ca61e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3070&q=80',
		'https://images.unsplash.com/photo-1470252649378-9c29740c9fa8?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3540&q=80',
		'https://images.unsplash.com/photo-1554080353-a576cf803bda?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3387&q=80',
		'https://images.unsplash.com/photo-1505144808419-1957a94ca61e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3070&q=80',
		'https://images.unsplash.com/photo-1554080353-a576cf803bda?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3387&q=80',
		'https://images.unsplash.com/photo-1505144808419-1957a94ca61e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3070&q=80',
		'https://images.unsplash.com/photo-1470252649378-9c29740c9fa8?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3540&q=80',
		'https://images.unsplash.com/photo-1554080353-a576cf803bda?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3387&q=80',
		'https://images.unsplash.com/photo-1505144808419-1957a94ca61e?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=3070&q=80'
	];

	const items = [
		{
			title: 'The Dawn of Innovation',
			description: 'Explore the birth of groundbreaking ideas and inventions.',
			icon: ClipboardCopy
		},
		{
			title: 'The Digital Revolution',
			description: 'Dive into the transformative power of technology.',
			icon: File
		},
		{
			title: 'The Art of Design',
			description: 'Discover the beauty of thoughtful and functional design.',
			icon: FileSignature
		},
		{
			title: 'The Power of Communication',
			description: 'Understand the impact of effective communication in our lives.',
			icon: Table
		},
		{
			title: 'The Pursuit of Knowledge',
			description: 'Join the quest for understanding and enlightenment.',
			icon: Waves
		},
		{
			title: 'The Joy of Creation',
			description: 'Experience the thrill of bringing ideas to life.',
			icon: Box
		},
		{
			title: 'The Spirit of Adventure',
			description: 'Embark on exciting journeys and thrilling discoveries.',
			icon: Boxes
		}
	];

	const products = [
		{
			title: 'Moonbeam',
			link: 'https://gomoonbeam.com',
			thumbnail: 'https://aceternity.com/images/products/thumbnails/new/moonbeam.png'
		},
		{
			title: 'Cursor',
			link: 'https://cursor.so',
			thumbnail: 'https://aceternity.com/images/products/thumbnails/new/cursor.png'
		},
		{
			title: 'Rogue',
			link: 'https://userogue.com',
			thumbnail: 'https://aceternity.com/images/products/thumbnails/new/rogue.png'
		},

		{
			title: 'Editorially',
			link: 'https://editorially.org',
			thumbnail: 'https://aceternity.com/images/products/thumbnails/new/editorially.png'
		},
		{
			title: 'Editrix AI',
			link: 'https://editrix.ai',
			thumbnail: 'https://aceternity.com/images/products/thumbnails/new/editrix.png'
		},
		{
			title: 'Pixel Perfect',
			link: 'https://app.pixelperfect.quest',
			thumbnail: 'https://aceternity.com/images/products/thumbnails/new/pixelperfect.png'
		},

		{
			title: 'Algochurn',
			link: 'https://algochurn.com',
			thumbnail: 'https://aceternity.com/images/products/thumbnails/new/algochurn.png'
		},
		{
			title: 'Aceternity UI',
			link: 'https://ui.aceternity.com',
			thumbnail: 'https://aceternity.com/images/products/thumbnails/new/aceternityui.png'
		},
		{
			title: 'Tailwind Master Kit',
			link: 'https://tailwindmasterkit.com',
			thumbnail: 'https://aceternity.com/images/products/thumbnails/new/tailwindmasterkit.png'
		},
		{
			title: 'SmartBridge',
			link: 'https://smartbridgetech.com',
			thumbnail: 'https://aceternity.com/images/products/thumbnails/new/smartbridge.png'
		},
		{
			title: 'Renderwork Studio',
			link: 'https://renderwork.studio',
			thumbnail: 'https://aceternity.com/images/products/thumbnails/new/renderwork.png'
		},

		{
			title: 'Creme Digital',
			link: 'https://cremedigital.com',
			thumbnail: 'https://aceternity.com/images/products/thumbnails/new/cremedigital.png'
		},
		{
			title: 'Golden Bells Academy',
			link: 'https://goldenbellsacademy.com',
			thumbnail: 'https://aceternity.com/images/products/thumbnails/new/goldenbellsacademy.png'
		},
		{
			title: 'Invoker Labs',
			link: 'https://invoker.lol',
			thumbnail: 'https://aceternity.com/images/products/thumbnails/new/invoker.png'
		},
		{
			title: 'E Free Invoice',
			link: 'https://efreeinvoice.com',
			thumbnail: 'https://aceternity.com/images/products/thumbnails/new/efreeinvoice.png'
		}
	];
</script>

<HeroParallax {products}>
	<div class="relative h-screen w-full overflow-hidden">
		<div class="flex h-full items-center justify-between px-8 md:px-16">
			<div class="w-1/2">
				<h1 class="mb-4 text-4xl font-bold text-white md:text-6xl">
					Crafting Digital Experiences That Elevate Your Brand
				</h1>
				<p class="mb-8 text-xl text-white">
					We build fast, beautiful, and functional websites that drive results.
				</p>
			</div>
			<div class="w-1/2 max-w-md rounded-lg bg-white/10 p-8 backdrop-blur-md">
				<!-- <form method="POST" use:enhance>
					<Form.Field {form} name="username">
						<Form.Control let:attrs>
							<Form.Label>Username</Form.Label>
							<Input {...attrs} bind:value={$formData.username} />
						</Form.Control>
						<Form.Description>This is your public display name.</Form.Description>
						<Form.FieldErrors />
					</Form.Field>
					<Form.Button>Submit</Form.Button>
				</form> -->
			</div>
		</div>
	</div>
</HeroParallax>

<!-- <div
	class="relative flex h-[40rem] w-full flex-col items-center justify-center rounded-md bg-neutral-950 md:px-32 antialiased"
>
	<div class="mx-auto max-w-2xl p-4">
		<h2
			class="relative z-10 bg-gradient-to-b from-neutral-200 to-neutral-600 bg-clip-text text-center font-sans text-lg font-bold text-transparent md:text-7xl"
		>
			Join the waitlist
		</h2>
		<p></p>
		<p class="relative z-10 mx-auto my-2 max-w-lg text-center text-sm text-neutral-500">
			Welcome to MailJet, the best transactional email service on the web. We provide reliable,
			scalable, and customizable email solutions for your business. Whether you&apos;re sending
			order confirmations, password reset emails, or promotional campaigns, MailJet has got you
			covered.
		</p>
		<input
			type="text"
			placeholder="hi@manuarora.in"
			class="relative z-10 mt-4 w-full rounded-lg border border-neutral-800 bg-neutral-950 p-2 placeholder:text-neutral-700 focus:ring-2 focus:ring-teal-500"
		/>
	</div>
	<BackgroundBeams />
</div> -->

<!-- <BentoGrid className="max-w-4xl mx-auto">
	{#each items as item, i (i)}
		<BentoGridItem
			title={item.title}
			description={item.description}
			className={i === 3 || i === 6 ? 'md:col-span-2' : ''}
		>
			<div
				slot="header"
				class="flex h-full min-h-[6rem] w-full flex-1 rounded-xl bg-gradient-to-br from-neutral-200 to-neutral-100 dark:from-neutral-900 dark:to-neutral-800"
			></div>
			<svelte:component this={item.icon} slot="icon" class="h-4 w-4 text-neutral-500" />
		</BentoGridItem>
	{/each}
</BentoGrid>


<ParallaxScroll {images} /> -->
