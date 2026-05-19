<script>
    import { base } from "$app/paths";

    import {
        Button,
        ButtonSet,
        Column,
        Grid,
        Row,
        Stack,
        Tag,
        Tile,
    } from "carbon-components-svelte";

    let hasProgress = $state(false);

    $effect(() => {
        const savedAnswers = sessionStorage.getItem("test-answers");
        const savedQuestions = sessionStorage.getItem("test-questions");

        hasProgress = !!savedAnswers && !!savedQuestions;
    });

    function startNewTest() {
        sessionStorage.removeItem("test-current-index");
        sessionStorage.removeItem("test-questions");
        sessionStorage.removeItem("test-answers");

        window.location.href = `${base}/test`;
    }
</script>

<Grid>
    <Row>
        <Column lg={6}>
            <Stack gap={6}>
                <Tile>
                    <Stack gap={5}>
                        <h1>Personality Test</h1>

                        <p>
                            This test helps students discover which study direction may
                            fit their interests strengths and future goals.
                        </p>

                        <p>
                            You will answer different questions about how you like to work
                            think create and interact with others. At the end of the test
                            you will receive a profile based on your answers.
                        </p>

                        <div class="tags">
                            <Tag type="blue">Achiever</Tag>
                            <Tag type="green">Thinker</Tag>
                            <Tag type="purple">Socialforce</Tag>
                            <Tag type="cyan">Creative</Tag>
                            <Tag type="magenta">Entrepreneur</Tag>
                        </div>

                        <p>
                            Each question has five answer options from strongly disagree
                            to strongly agree. The test calculates which domain matches
                            you best and also shows your scores for the other domains.
                        </p>

                        <p>
                            The questions are shown in English. You can also view the
                            Indonesian translation when you need extra help understanding
                            a question.
                        </p>
                    </Stack>
                </Tile>

                {#if hasProgress}
                    <ButtonSet style="width: 100%;">
                        <Button
                                kind="primary"
                                style="width: 50%; max-width: 100%;"
                                on:click={startNewTest}
                        >
                            New test
                        </Button>

                        <Button
                                kind="secondary"
                                style="width: 50%; max-width: 100%;"
                                href={`${base}/test`}
                        >
                            Previous test
                        </Button>
                    </ButtonSet>
                {:else}
                    <Button
                            href={`${base}/test`}
                            kind="primary"
                            style="width: 100%; max-width: 100%;"
                    >
                        Start test
                    </Button>
                {/if}
            </Stack>
        </Column>
    </Row>
</Grid>

<style>
    .tags {
        display: flex;
        flex-wrap: wrap;
        gap: 0.5rem;
    }
</style>