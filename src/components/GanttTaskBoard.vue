<template>
	<div class="content-body">
		<!--$$ REMOTE DATA -->
		<BryntumProjectModel ref="project" />

		<!--$$ LOCAL DATA -->
		<!--<BryntumProjectModel ref="project" :tasks="tasks" />-->

		<BryntumGantt ref="bryntumGantt" :project="project" v-bind="ganttConfig" />

		<BryntumTaskBoard ref="bryntumTaskBoard" :project="project" v-bind="taskBoardConfig" />
	</div>
</template>

<script setup>
	/* eslint-disable */
	import { ref, reactive } from 'vue';
	import { BryntumGantt, BryntumProjectModel } from '@bryntum/gantt-vue-3';
	import { BryntumTaskBoard } from '@bryntum/taskboard-vue-3';

	// $$ REMOTE DATA
	const project = ref({
		autoLoad: true,
		transport: {
			load: {
				url: `/data.json`,
				method: 'GET'
			}
		}
	});

	// $$ LOCAL DATA
	//const project = ref(null);

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
			columnField: 'status'
		};
	};
	const taskBoardConfig = reactive(useTaskBoardConfig());

	//tasks
	//$$ LOCAL DATA
	//const tasks = [
	//	{
	//		"id": 127,
	//		"parentId": null,
	//		"leaf": false,
	//		"name": "New task 1",
	//		"startDate": "2022-07-13T23:00:00",
	//		"endDate": "2022-07-14T00:00:00",
	//		"duration": 1.00,
	//		"durationUnit": "hour",
	//		"percentDone": 0.00,
	//		"schedulingMode": "Normal",
	//		"baselineStartDate": null,
	//		"baselineEndDate": null,
	//		"baselinePercentDone": null,
	//		"cls": "",
	//		"index": null,
	//		"expanded": true,
	//		"effort": 1.00,
	//		"effortUnit": "hour",
	//		"note": null,
	//		"constraintType": null,
	//		"constraintDate": null,
	//		"manuallyScheduled": false,
	//		"draggable": true,
	//		"resizable": true,
	//		"rollup": false,
	//		"showInTimeline": false,
	//		"color": null,
	//		"deadlineDate": null,
	//		"children": [
	//			{
	//				"id": 125,
	//				"parentId": "127",
	//				"leaf": true,
	//				"name": "New Task 1.1",
	//				"startDate": "2022-07-13T23:00:00",
	//				"endDate": "2022-07-13T23:30:00",
	//				"duration": 0.50,
	//				"durationUnit": "hour",
	//				"percentDone": 0.00,
	//				"schedulingMode": "Normal",
	//				"baselineStartDate": null,
	//				"baselineEndDate": null,
	//				"baselinePercentDone": null,
	//				"cls": "",
	//				"index": null,
	//				"expanded": true,
	//				"effort": 0.50,
	//				"effortUnit": "hour",
	//				"note": null,
	//				"constraintType": null,
	//				"constraintDate": null,
	//				"manuallyScheduled": false,
	//				"draggable": true,
	//				"resizable": true,
	//				"rollup": false,
	//				"showInTimeline": false,
	//				"color": null,
	//				"deadlineDate": null,
	//				"children": [],
	//				"pitProgramId": null,
	//				"pitPlanningDepartmentId": 1,
	//				"pitPlanningDepartmentGroupId": 7,
	//				"pitTaskTypeId": null,
	//				"pitTxDateTime": null,
	//				"statusId": 1,
	//				"status": "Open",
	//				"pitDeliveryDate": null,
	//				"pitExternalReference": null,
	//				"pitPlatformId": null,
	//				"pitLink": null,
	//				"pitSequence": null,
	//				"pitProgramEpisodeIds": [],
	//				"Id": 125
	//			},
	//			{
	//				"id": 126,
	//				"parentId": "127",
	//				"leaf": true,
	//				"name": "New Task 1.2",
	//				"startDate": "2022-07-13T23:30:00",
	//				"endDate": "2022-07-14T00:00:00",
	//				"duration": 0.50,
	//				"durationUnit": "hour",
	//				"percentDone": 0.00,
	//				"schedulingMode": "Normal",
	//				"baselineStartDate": null,
	//				"baselineEndDate": null,
	//				"baselinePercentDone": null,
	//				"cls": "",
	//				"index": null,
	//				"expanded": true,
	//				"effort": 0.50,
	//				"effortUnit": "hour",
	//				"note": null,
	//				"constraintType": "startnoearlierthan",
	//				"constraintDate": "2022-07-13T23:30:00",
	//				"manuallyScheduled": false,
	//				"draggable": true,
	//				"resizable": true,
	//				"rollup": false,
	//				"showInTimeline": false,
	//				"color": null,
	//				"deadlineDate": null,
	//				"children": [],
	//				"pitProgramId": null,
	//				"pitPlanningDepartmentId": 1,
	//				"pitPlanningDepartmentGroupId": 7,
	//				"pitTaskTypeId": null,
	//				"pitTxDateTime": null,
	//				"statusId": 1,
	//				"status": "Planned",
	//				"pitDeliveryDate": null,
	//				"pitExternalReference": null,
	//				"pitPlatformId": null,
	//				"pitLink": null,
	//				"pitSequence": null,
	//				"pitProgramEpisodeIds": [],
	//				"Id": 126
	//			}
	//		],
	//		"pitProgramId": null,
	//		"pitPlanningDepartmentId": 1,
	//		"pitPlanningDepartmentGroupId": 7,
	//		"pitTaskTypeId": null,
	//		"pitTxDateTime": null,
	//		"statusId": 1,
	//		"status": "Open",
	//		"pitDeliveryDate": null,
	//		"pitExternalReference": null,
	//		"pitPlatformId": null,
	//		"pitLink": null,
	//		"pitSequence": null,
	//		"pitProgramEpisodeIds": [],
	//		"Id": 127
	//	},
	//	{
	//		"id": 128,
	//		"parentId": null,
	//		"leaf": false,
	//		"name": "New Task 2",
	//		"startDate": "2022-07-14T00:00:00",
	//		"endDate": "2022-07-14T01:00:00",
	//		"duration": 1.00,
	//		"durationUnit": "hour",
	//		"percentDone": 0.00,
	//		"schedulingMode": "Normal",
	//		"baselineStartDate": null,
	//		"baselineEndDate": null,
	//		"baselinePercentDone": null,
	//		"cls": "",
	//		"index": null,
	//		"expanded": true,
	//		"effort": 1.00,
	//		"effortUnit": "hour",
	//		"note": null,
	//		"constraintType": null,
	//		"constraintDate": null,
	//		"manuallyScheduled": false,
	//		"draggable": true,
	//		"resizable": true,
	//		"rollup": false,
	//		"showInTimeline": false,
	//		"color": null,
	//		"deadlineDate": null,
	//		"children": [
	//			{
	//				"id": 129,
	//				"parentId": "128",
	//				"leaf": true,
	//				"name": "New task 2.2",
	//				"startDate": "2022-07-14T00:30:00",
	//				"endDate": "2022-07-14T01:00:00",
	//				"duration": 0.50,
	//				"durationUnit": "hour",
	//				"percentDone": 0.00,
	//				"schedulingMode": "Normal",
	//				"baselineStartDate": null,
	//				"baselineEndDate": null,
	//				"baselinePercentDone": null,
	//				"cls": "",
	//				"index": null,
	//				"expanded": true,
	//				"effort": 0.50,
	//				"effortUnit": "hour",
	//				"note": null,
	//				"constraintType": null,
	//				"constraintDate": null,
	//				"manuallyScheduled": false,
	//				"draggable": true,
	//				"resizable": true,
	//				"rollup": false,
	//				"showInTimeline": false,
	//				"color": null,
	//				"deadlineDate": null,
	//				"children": [],
	//				"pitProgramId": null,
	//				"pitPlanningDepartmentId": 1,
	//				"pitPlanningDepartmentGroupId": 7,
	//				"pitTaskTypeId": null,
	//				"pitTxDateTime": null,
	//				"statusId": 1,
	//				"status": "Open",
	//				"pitDeliveryDate": null,
	//				"pitExternalReference": null,
	//				"pitPlatformId": null,
	//				"pitLink": null,
	//				"pitSequence": null,
	//				"pitProgramEpisodeIds": [],
	//				"Id": 129
	//			},
	//			{
	//				"id": 130,
	//				"parentId": "128",
	//				"leaf": true,
	//				"name": "New task 2.1",
	//				"startDate": "2022-07-14T00:00:00",
	//				"endDate": "2022-07-14T00:30:00",
	//				"duration": 0.50,
	//				"durationUnit": "hour",
	//				"percentDone": 0.00,
	//				"schedulingMode": "Normal",
	//				"baselineStartDate": null,
	//				"baselineEndDate": null,
	//				"baselinePercentDone": null,
	//				"cls": "",
	//				"index": null,
	//				"expanded": true,
	//				"effort": 0.50,
	//				"effortUnit": "hour",
	//				"note": null,
	//				"constraintType": null,
	//				"constraintDate": null,
	//				"manuallyScheduled": false,
	//				"draggable": true,
	//				"resizable": true,
	//				"rollup": false,
	//				"showInTimeline": false,
	//				"color": null,
	//				"deadlineDate": null,
	//				"children": [],
	//				"pitProgramId": null,
	//				"pitPlanningDepartmentId": 1,
	//				"pitPlanningDepartmentGroupId": 7,
	//				"pitTaskTypeId": null,
	//				"pitTxDateTime": null,
	//				"statusId": 1,
	//				"status": "Open",
	//				"pitDeliveryDate": null,
	//				"pitExternalReference": null,
	//				"pitPlatformId": null,
	//				"pitLink": null,
	//				"pitSequence": null,
	//				"pitProgramEpisodeIds": [],
	//				"Id": 130
	//			}
	//		],
	//		"pitProgramId": null,
	//		"pitPlanningDepartmentId": 1,
	//		"pitPlanningDepartmentGroupId": 7,
	//		"pitTaskTypeId": null,
	//		"pitTxDateTime": null,
	//		"statusId": 1,
	//		"status": "Open",
	//		"pitDeliveryDate": null,
	//		"pitExternalReference": null,
	//		"pitPlatformId": null,
	//		"pitLink": null,
	//		"pitSequence": null,
	//		"pitProgramEpisodeIds": [],
	//		"Id": 128
	//	},
	//	{
	//		"id": 131,
	//		"parentId": null,
	//		"leaf": true,
	//		"name": "New task",
	//		"startDate": "2022-07-13T23:00:00",
	//		"endDate": "2022-07-14T00:00:00",
	//		"duration": 1.00,
	//		"durationUnit": "hour",
	//		"percentDone": 0.00,
	//		"schedulingMode": "Normal",
	//		"baselineStartDate": null,
	//		"baselineEndDate": null,
	//		"baselinePercentDone": null,
	//		"cls": "",
	//		"index": null,
	//		"expanded": true,
	//		"effort": 0.50,
	//		"effortUnit": "hour",
	//		"note": null,
	//		"constraintType": null,
	//		"constraintDate": null,
	//		"manuallyScheduled": false,
	//		"draggable": true,
	//		"resizable": true,
	//		"rollup": false,
	//		"showInTimeline": false,
	//		"color": null,
	//		"deadlineDate": null,
	//		"children": [],
	//		"pitProgramId": null,
	//		"pitPlanningDepartmentId": 1,
	//		"pitPlanningDepartmentGroupId": 7,
	//		"pitTaskTypeId": null,
	//		"pitTxDateTime": null,
	//		"statusId": 1,
	//		"status": "Open",
	//		"pitDeliveryDate": null,
	//		"pitExternalReference": null,
	//		"pitPlatformId": null,
	//		"pitLink": null,
	//		"pitSequence": null,
	//		"pitProgramEpisodeIds": [],
	//		"Id": 131
	//	}
	//];

</script>

<style>
	.content-body {
		background-color: var(--c-grey-lighter);
		height: calc(100% - 52px);
		width: 100vw;
	}
</style>
