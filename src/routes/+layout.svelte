<script lang="ts">
	import favicon from "$lib/assets/favicon.svg";
	import "carbon-components-svelte/css/all.css";

	import {
		Content,
		Header,
		HeaderGlobalAction,
		HeaderUtilities,
		LocalStorage,
		Modal,
		RadioTile,
		SkipToContent,
		Theme,
		TileGroup,
	} from "carbon-components-svelte";

	import Sun from "carbon-icons-svelte/lib/Sun.svelte";
	import Moon from "carbon-icons-svelte/lib/Moon.svelte";
	import Language from "carbon-icons-svelte/lib/Language.svelte";

	let { children } = $props();

	let languageModalOpen = $state(false);

	let isDarkMode = $state(false);

	let language = $state("english");
	let selectedLanguage = $state(language);

	const currentTheme = $derived(isDarkMode ? "g90" : "white");
	const themeIcon = $derived(isDarkMode ? Sun : Moon);
	const themeText = $derived(isDarkMode ? "Light mode" : "Dark mode");

	function openLanguageModal() {
		selectedLanguage = language;
		languageModalOpen = true;
	}
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<LocalStorage key="dark-mode" bind:value={isDarkMode} />
<LocalStorage key="language" bind:value={language} />

<Theme theme={currentTheme} />

<Header
		companyName="Yayasan Dana Punia"
		platformName="Personality test"
>
	<svelte:fragment slot="skipToContent">
		<SkipToContent />
	</svelte:fragment>

	<HeaderUtilities>
		<HeaderGlobalAction
				icon={themeIcon}
				iconDescription={themeText}
				tooltipAlignment="end"
				on:click={() => {
                isDarkMode = !isDarkMode;
            }}
		/>

<!--		<HeaderGlobalAction-->
<!--				icon={Language}-->
<!--				iconDescription="Language"-->
<!--				tooltipAlignment="end"-->
<!--				on:click={openLanguageModal}-->
<!--		/>-->
	</HeaderUtilities>
</Header>

<Modal
		size="xs"
		bind:open={languageModalOpen}
		modalHeading="Language"
		primaryButtonText="Save"
		secondaryButtonText="Cancel"
		on:click:button--secondary={() => {
        selectedLanguage = language;
        languageModalOpen = false;
    }}
		on:submit={() => {
        language = selectedLanguage;
        languageModalOpen = false;
    }}
>
	<TileGroup
			name="language"
			selected={selectedLanguage}
			on:select={(event) => {
       		selectedLanguage = event.detail;
    		}}
	>
		<RadioTile value="english" tabindex="-1">
			English
		</RadioTile>

		<RadioTile value="indonesian" tabindex="-1">
			Bahasa Indonesia
		</RadioTile>
	</TileGroup>
</Modal>

<Content>
	{@render children()}
</Content>