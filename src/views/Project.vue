<template>
	<div>
		<div v-if="project" class="columns">
			<div>
				<div class="sidebar">
					<router-link to="/">Project List</router-link>
					<project-settings></project-settings>
					<launchers></launchers>
					<tasks></tasks>
				</div>
			</div>
			<div>
				<div class="main">
					<compiler></compiler>
					<presets></presets> 
				</div>
			</div>
		</div>
		<div>
			<h3>Project does not exists</h3>
			<router-link to="/">Return Back</router-link>
		</div>
	</div>
</template>

<script>
	import { find } from "lodash/collection"
	import { matches } from "lodash/util"
	import { mapField } from "@/libs/vuex-field-mapper.js"
	import ProjectSettings from "@/components/ProjectSettings"
	import Launchers from "@/components/Launchers"
	import Tasks from "@/components/Tasks"
	import Compiler from "@/components/Compiler"
	import Presets from "@/components/Presets"

	export default {
		computed: {
			projectId() {
				return this.$route.params.id;
			},
			...mapField({
				project (state) {
					return find(state.projects.items, matches({ id: this.projectId }));
				}
			})
		},
		components: { ProjectSettings, Launchers, Tasks, Compiler, Presets }
	}
</script>

<style scoped>
	.columns {
		display: grid;
		grid-template-columns: 300px auto;
		grid-auto-rows: minmax(100px, 100vh);
	}
	.sidebar {
		padding: 5px;
		height: 100%;
		overflow: auto;
		background: #eee;
		box-sizing: border-box;
	}
	.main {
		padding: 5px;
		height: 100%;
		overflow: auto;
		box-sizing: border-box;
	}
</style>

