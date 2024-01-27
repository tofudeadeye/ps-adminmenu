<script>
	import { slide } from 'svelte/transition'
	import VehicleProperty from './VehicleProperty.svelte'

	export let data
	export let id

	let dropdownActive
</script>

<div
	class=" bg-tertiary rounded-[0.5vh] {dropdownActive
		? ''
		: 'hover:bg-opacity-90'}"
>
	<button
		class="w-full h-[4.5vh] flex items-center justify-between px-[1.5vh]"
		on:click={() => (dropdownActive = !dropdownActive)}
	>
		<div class="flex items-center gap-[1vh]">
			<p>{data.label}</p>
		</div>
		<i class="fas fa-angle-{dropdownActive ? 'down' : 'right'}" />
	</button>

	{#if dropdownActive}
		<div
			class="w-full rounded-b-[1vh] p-[1.5vh] flex flex-col gap-[1vh] justify-start items-start"
			transition:slide={{ duration: 150 }}
		>
			{#each data.dropdown as i}
				{#if i.option === 'dropdown'}
					<VehicleProperty
						data={i.data}
						label={i.label}
						modAttr={i.modAttr}
						colorpicker={false}
					/>
				{:else if i.option === 'colorpicker'}
					<VehicleProperty
						data={i.data}
						label={i.label}
						modAttr={i.modAttr}
						colorpicker={true}
					/>
				{/if}
			{/each}
		</div>
	{/if}
</div>
