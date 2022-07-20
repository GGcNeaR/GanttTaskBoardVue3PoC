<template>
	<GanttTaskBoard />
</template>

<script>
	import GanttTaskBoard from './components/GanttTaskBoard.vue'

export default {
	name: 'App',
	components: {
		GanttTaskBoard
	}
}
</script>


<style lang="scss">
	@import "@/assets/css/variables.scss";
    @import "@/assets/vendor/bryntum/sass/themes/stockholm.scss";
</style>


<style lang="postcss">
    @import "@bryntum/taskboard/taskboard.stockholm.css";

    #app {
      width: 100%;
      height: 100vh;
      display: grid;
      grid-template-rows: min-content 1fr var(--space-6);
      font: var(--font-base);
      color: var(--c-grey-darkest);
      background-color: var(--c-grey-lighter);
    }

</style>
