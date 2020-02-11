<template>
<section class="content" v-cloak>
	<div class="row">
		<div class="col-sm-6">
			<div class="row">
				<div class="col-sm-6">
					<sensor entity_id="sensor.particulate_bme280_temperature" title="Indoor Temperature" icon="fa-home" color-class="bg-red"></sensor>
				</div>
				<div class="col-sm-6">
					<light entity_id="light.light"></light>
				</div>
			</div>
		</div>
		<div class="col-sm-6">
			<div v-if="entities['sensor.bom_forecast_0']" class="box box-widget widget-user">
				<!-- Add the bg color to the header using any of the bg-* classes -->
				<div class="widget-user-header bg-black" style="background: url('images/fountain.jpg') center center; background-size: cover; height: 92px;">
				<h3 class="widget-user-username" style="font-weight: bold;">Current Conditions</h3>
				<h5 class="widget-user-desc">Home</h5>
				</div>
				<div class="widget-user-image" style="top: 45px;">
				<img class="img-circle" :src="entities['sensor.bom_forecast_0']['attributes']['entity_picture']" :alt="entities['sensor.bom_forecast_0']['state']" style="background-color:white;">
				</div>
				<div class="box-footer" style="padding-top: 15px;">
					<div class="row">
						<div class="col-sm-3 border-right">
						<div class="description-block" v-if="entities['sensor.today_temp_bom']">
							<h5 class="description-header">{{entities['sensor.today_temp_bom']['state']}}{{entities['sensor.today_temp_bom']['attributes']['unit_of_measurement']}}</h5>
							<span class="description-text">TEMP</span>
						</div>
						</div>
						<div class="col-sm-3 border-right">
						<div class="description-block" v-if="entities['sensor.bom_fremantle_relative_humidity']">
							<h5 class="description-header">{{entities['sensor.bom_fremantle_relative_humidity']['state']}}{{entities['sensor.bom_fremantle_relative_humidity']['attributes']['unit_of_measurement']}}</h5>
							<span class="description-text">HUMIDITY</span>
						</div>
						</div>
						<div class="col-sm-3 border-right">
						<div class="description-block" v-if="entities['sensor.bom_fremantle_possible_rainfall_0']">
							<h5 class="description-header">{{entities['sensor.bom_fremantle_possible_rainfall_0']['state']}}{{entities['sensor.bom_fremantle_possible_rainfall_0']['attributes']['unit_of_measurement']}}</h5>
							<span class="description-text">Rain Today</span>
						</div>
						</div>
						<div class="col-sm-3">
						<div class="description-block" v-if="entities['sensor.bom_fremantle_wind_speed_kmh']">
							<h5 class="description-header">{{entities['sensor.bom_fremantle_wind_speed_kmh']['state'].substring(0,1)}} {{entities['sensor.bom_fremantle_wind_speed_kmh']['state']}}{{entities['sensor.bom_fremantle_wind_speed_kmh']['attributes']['unit_of_measurement']}}</h5>
							<span class="description-text">WIND</span>
						</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
	
		<div class="col-sm-6">
			<action title="Baby's Bedtime" icon="fa-bed" description="Dims living room lights, turns on cabinet lights." entity_id="scene.baby_bedtime"></action>
			<action title="Goodbye" icon="fa-automobile" description="Turns on porch light for 3 minutes (after dark)." entity_id="script.goodbye_lights"></action>
			<action title="Goodnight" icon="fa-bed" description="Turns off all lights. Turns on dim cabinet lights." entity_id="script.goodnight"></action>
		</div>
	</div>
</section>
</template>

<script>
module.exports = {
	computed: {
		entities() {
			return this.$store.state.entities;
		},
		secrets() {
			return this.$parent.secrets;
		}
	},
}
</script>