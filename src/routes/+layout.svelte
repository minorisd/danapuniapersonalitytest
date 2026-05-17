<script lang="ts">
	import favicon from "$lib/assets/favicon.svg";
	import "carbon-components-svelte/css/all.css";

	import {
		Content,
		Header,
		HeaderAction,
		HeaderPanelDivider,
		HeaderPanelLink,
		HeaderPanelLinks,
		HeaderUtilities,
		SkipToContent, Theme,
	} from "carbon-components-svelte";

	import SettingsAdjust from "carbon-icons-svelte/lib/SettingsAdjust.svelte";

	let { children } = $props();

	let isOpen = $state(false);
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<!--<Theme-->
<!--		theme="g90"-->
<!--		tokens={{-->
<!--    // Interactive elements-->
<!--    "interactive-01": "#d02670", // Primary button background-->
<!--    "hover-primary": "#ee5396", // Primary button hover-->
<!--    "active-primary": "#9f1853", // Primary button active-->
<!--    "interactive-02": "#6f6f6f", // Secondary button background-->
<!--    "hover-secondary": "#5e5e5e", // Secondary button hover-->

<!--    // Links-->
<!--    "link-01": "#ff6eb3", // Link text color-->

<!--    // Tags-->
<!--    "tag-background-blue": "#4a1942", // Tag background-->
<!--    "tag-color-blue": "#ffb3d9", // Tag text color-->

<!--    // Form elements-->
<!--    "field-01": "#2d2d2d", // Input field background-->
<!--    "ui-01": "#2d2d2d", // Tile background-->
<!--    focus: "#ff6eb3", // Focus indicator color-->

<!--    // Text colors-->
<!--    "text-01": "#ffffff", // Primary text-->
<!--    "text-02": "#c6c6c6", // Secondary text-->

<!--    // Notification colors-->
<!--    "support-04": "#a855f7", // Info notification color-->
<!--  }}-->
<!--/>-->

<Header
		companyName="Yayasan Dana Punia"
		platformName="Personality test"
>
	<svelte:fragment slot="skipToContent">
		<SkipToContent />
	</svelte:fragment>

	<HeaderUtilities>
		<HeaderAction
				bind:isOpen
				icon={SettingsAdjust}
				iconDescription="Settings"
				text="Settings"
				tooltipAlignment="start"
				on:open={() => isOpen = true}
				on:close={() => isOpen = false}
		>
			<HeaderPanelLinks>
				<HeaderPanelDivider>Settings</HeaderPanelDivider>
				<HeaderPanelLink>language</HeaderPanelLink>
				<HeaderPanelLink>previous results</HeaderPanelLink>
			</HeaderPanelLinks>
		</HeaderAction>
	</HeaderUtilities>
</Header>

<Content>
	{@render children()}
</Content>