<script>
	import { slide } from 'svelte/transition'
	import { onMount } from 'svelte'
	import { SendNUI } from '@utils/SendNUI'
	import ColorPicker from 'svelte-awesome-color-picker'
	import { VEHICLE_PROPS } from '@store/vehicle_dev'

	export let data
	export let label
	export let modAttr
	export let colorpicker = false

	let vehProps
	let selectedItem = null
	let search = ''
	let rgb
	let searchInputFocused = false
	let DataDropdownActive = false

	onMount(() => {
		if (selectedItem instanceof Object && selectedItem.label != null) {
			search = selectedItem.label
		}
	})

	VEHICLE_PROPS.subscribe((value) => {
		vehProps = value
		selectedItem = data.find((o) => o.value === vehProps[modAttr])
		// console.log(label + ' (' + modAttr + '): ', selectedItem)
	})

	function updateColorPicker(event) {
		rgb = [event.detail.rgb.r, event.detail.rgb.g, event.detail.rgb.b]
	}

	function selectData(item) {
		vehProps[modAttr] = item.value
		VEHICLE_PROPS.set(vehProps)
		// todo: do we save to server here?

		SendNUI('setVehicleProps', {
			data: vehProps,
		})

		search = item.label
		DataDropdownActive = false
	}

	function handleInputFocus() {
		searchInputFocused = true
		DataDropdownActive = true
		search = ''
	}

	function handleInputBlur() {
		if (!searchInputFocused) {
			DataDropdownActive = false
		}
		searchInputFocused = false
	}
</script>

{#if colorpicker}
	<div class="pt-[1vh]">
		<ColorPicker
			isDialog={false}
			isAlpha={false}
			isTextInput={true}
			textInputModes={['rgb']}
			disableCloseClickOutside={true}
			--cp-bg-color={'bg-transparent'}
			--cp-border-color={'border-primary'}
			--cp-input-color={'#1a1b1e'}
			--focus-color={'border-primary'}
			--picker-width={'175px'}
			on:input={updateColorPicker}
			rgb={{ r: 0, b: 0, g: 0 }}
		/>
	</div>
	<button
		id="colorpicker"
		class="h-[3.8vh] px-[1.5vh] rounded-[0.5vh] bg-secondary hover:bg-opacity-90 border-[0.1vh] border-primary"
		on:click={() => {
			selectData({ value: rgb })
		}}
	>
		<p>Apply Changes</p>
	</button>
{:else}
	<div
		class="w-full flex flex-col bg-secondary rounded-[0.5vh] border-[0.1vh] border-primary"
	>
		<div
			class="w-full h-[3.8vh] px-[1vh] flex justify-between items-center"
		>
			<input
				type="text"
				placeholder={label}
				on:focus={handleInputFocus}
				on:blur={handleInputBlur}
				bind:value={search}
				class="h-full w-[90%] bg-transparent"
			/>
			<i
				class="fas fa-angle-{DataDropdownActive
					? 'down'
					: 'right'} text-[1.2vh]"
			></i>
		</div>

		{#if DataDropdownActive}
			<button
				class="w-full rounded-b-[0.5vh] flex flex-col max-h-[15vh] overflow-y-auto border-t border-primary scroll-visible"
				on:mouseenter={() => {
					searchInputFocused = true
				}}
				on:blur={() => {
					searchInputFocused = false
				}}
				transition:slide={{ duration: 150 }}
			>
				{#each data.filter((i) => i.label
						.toLowerCase()
						.includes(search.toLowerCase())) as i}
					<button
						class="w-full p-[0.5vh] flex justify-start text-start px-[1vh] gap-[0.5vh] hover:bg-tertiary"
						on:click={() => {
							selectData(i)
						}}
					>
						<p>{i.label}</p>
					</button>
				{/each}
			</button>
		{/if}
	</div>
{/if}
