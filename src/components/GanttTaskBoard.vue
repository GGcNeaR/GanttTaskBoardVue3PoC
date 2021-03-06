<template>
	<div class="content-body">
		<BryntumProjectModel ref="project" v-bind="projectConfig" />

		<BryntumGantt ref="bryntumGantt" :project="project" v-bind="ganttConfig" />

		<BryntumTaskBoard ref="bryntumTaskBoard" :project="project" v-bind="taskBoardConfig" />
	</div>
</template>

<script setup>
	import { ref, reactive, /*onMounted*/ } from 'vue';
	import { BryntumGantt, BryntumProjectModel } from '@bryntum/gantt-vue-3';
	import { BryntumTaskBoard } from '@bryntum/taskboard-vue-3';

	// Project
	const project = ref(null);

	const projectConfig = {
		autoLoad: true,
		transport: {
			load: {
				url: `/data.json`,
				method: 'GET'
			}
		}
	};

	// Gantt
	const bryntumGantt = ref(null);

	const useGanttConfig = () => {
		return {
			viewPreset: 'hourAndDay',
			rowHeight: 24,
			barMargin: 8,
			columns: [
				{ type: 'name', width: 250 },
				{ type: 'startdate', width: 100 },
				{ type: 'enddate', width: 100 },
				{ type: 'duration', width: 100 },
			]
		};
	};
	const ganttConfig = reactive(useGanttConfig());

	// TaskBoard
	const bryntumTaskBoard = ref(null);

	const useTaskBoardConfig = () => {
		return {
			useDomTransition: true,
			columns: [
				'Open',
				'Planned',
				'Can be started',
				'Started',
				'Done',
				'Cancelled'
			],
			columnField: 'status',
			features: {
				taskEdit: {
					// Prevent TaskBoard's task editor from showing and display Gantt's instead
					processItems({ taskRecord }) {
						bryntumGantt.value.instance.value.editTask(taskRecord); // replace this.gantt with your gantt reference

						return false;
					}
				}
			}
		};
	};
	const taskBoardConfig = reactive(useTaskBoardConfig());

</script>

<style>
	html, body,
	.content-body {
		background-color: var(--c-grey-lighter);
		height: 100%;
		width: 100vw;
	}
</style>
