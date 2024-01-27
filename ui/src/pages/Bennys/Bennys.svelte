<script lang="ts">
	import Header from '@components/Header.svelte'
	import VehiclePropertyContainer from './components/VehiclePropertyContainer.svelte'
	import { SendNUI } from '@utils/SendNUI'
	import { VEHICLE_DEV, VEHICLE_PROPS } from '@store/vehicle_dev'
	import {
		ARMOR,
		BRAKES,
		ENGINE,
		HORN,
		LIGHTS,
		PLATES,
		RESPRAY_PRIMARY,
		RESPRAY_SECONDARY,
		RESPRAY_PEARLESCENT,
		SUSPENSION,
		TRANSMISSION,
		TURBO,
		WINDOWS,
		WHEELS,
	} from './BennysMeta'

	let vehProps

	const vehPropsSubscribe = VEHICLE_PROPS.subscribe((value) => {
		vehProps = value
	})
</script>

<div class="h-full w-[99vh] px-[2vh]">
	<Header title={"Benny's"} hasSearch={false} hasLargeMenu={false} />
	<div
		class="w-full h-[90%] flex flex-col gap-[1vh] mt-[1vh] overflow-auto scroll-visble"
	>
		<div
			class="w-full bg-tertiary flex rounded-[0.5vh] flex-col gap-[2vh] rounded-[0.5vh] p-[2vh] font-medium"
		>
			<div>
				<p>Model: {$VEHICLE_DEV?.name}</p>
				<p>Hash: {$VEHICLE_DEV?.model}</p>
				<p>Plate: {$VEHICLE_DEV?.plate}</p>
			</div>
		</div>

		<div class="w-full pb-[1vh] pt-[1vh] flex flex-col gap-[1vh]">
			<div class="w-full bg-tertiary flex rounded-[0.5vh]">
				<button
					title="Fix Vehicle"
					class="h-[4.5vh] w-full rounded-l-[0.5vh] hover:bg-secondary
					relative
					before:content-[attr(data-tip)]
					before:absolute
					before:px-3 before:py-2
					before:left-1/2 before:-top-3
					before:w-max before:max-w-xs
					before:-translate-x-1/2 before:-translate-y-full
					before:bg-tertiary before:text-white
					before:rounded-md before:opacity-0
					before:translate-all

					after:absolute
					after:left-1/2 after:-top-3
					after:h-0 after:w-0
					after:-translate-x-1/2 after:border-8
					after:border-t-tertiary
					after:border-l-transparent
					after:border-b-transparent
					after:border-r-transparent
					after:opacity-0
					after:transition-all

					hover:before:opacity-100 hover:after:opacity-100
					"
					data-tip="Fix Vehicle"
					on:click={() =>
						SendNUI('clickButton', {
							data: 'fix_vehicle',
						})}
				>
					<i class="fas fa-wrench"></i>
				</button>
				<button
					title="Refuel"
					class="h-[4.5vh] w-full rounded-l-[0.5vh] hover:bg-secondary
					relative
					before:content-[attr(data-tip)]
					before:absolute
					before:px-3 before:py-2
					before:left-1/2 before:-top-3
					before:w-max before:max-w-xs
					before:-translate-x-1/2 before:-translate-y-full
					before:bg-tertiary before:text-white
					before:rounded-md before:opacity-0
					before:translate-all

					after:absolute
					after:left-1/2 after:-top-3
					after:h-0 after:w-0
					after:-translate-x-1/2 after:border-8
					after:border-t-tertiary
					after:border-l-transparent
					after:border-b-transparent
					after:border-r-transparent
					after:opacity-0
					after:transition-all

					hover:before:opacity-100 hover:after:opacity-100
					"
					data-tip="Refuel"
					on:click={() =>
						SendNUI('clickButton', {
							data: 'refuel_vehicle',
						})}
				>
					<i class="fas fa-gas-pump"></i>
				</button>
				<button
					title="Max Mods"
					class="h-[4.5vh] w-full rounded-l-[0.5vh] hover:bg-secondary
					relative
					before:content-[attr(data-tip)]
					before:absolute
					before:px-3 before:py-2
					before:left-1/2 before:-top-3
					before:w-max before:max-w-xs
					before:-translate-x-1/2 before:-translate-y-full
					before:bg-tertiary before:text-white
					before:rounded-md before:opacity-0
					before:translate-all

					after:absolute
					after:left-1/2 after:-top-3
					after:h-0 after:w-0
					after:-translate-x-1/2 after:border-8
					after:border-t-tertiary
					after:border-l-transparent
					after:border-b-transparent
					after:border-r-transparent
					after:opacity-0
					after:transition-all

					hover:before:opacity-100 hover:after:opacity-100
					"
					data-tip="Max Mods"
					on:click={() =>
						SendNUI('clickButton', {
							data: 'max_mods',
						})}
				>
					<i class="fas fa-truck-monster"></i>
				</button>
			</div>
		</div>

		<VehiclePropertyContainer data={ARMOR} id="armor" />
		<VehiclePropertyContainer data={BRAKES} id="brakes" />
		<VehiclePropertyContainer data={ENGINE} id="engine" />
		<VehiclePropertyContainer data={HORN} id="horn" />
		<VehiclePropertyContainer data={LIGHTS} id="lights" />
		<VehiclePropertyContainer data={PLATES} id="plates" />
		<VehiclePropertyContainer data={RESPRAY_PRIMARY} id="respray_primary" />
		<VehiclePropertyContainer
			data={RESPRAY_SECONDARY}
			id="respray_secondary"
		/>
		<VehiclePropertyContainer
			data={RESPRAY_PEARLESCENT}
			id="respray_pearlescent"
		/>
		<VehiclePropertyContainer data={SUSPENSION} id="suspension" />
		<VehiclePropertyContainer data={TRANSMISSION} id="transmission" />
		<VehiclePropertyContainer data={TURBO} id="turbo" />
		<VehiclePropertyContainer data={WINDOWS} id="windows" />
		<VehiclePropertyContainer data={WHEELS} id="wheels" />
	</div>
</div>
