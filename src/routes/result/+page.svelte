<script lang="ts">
    import { base } from "$app/paths";

    import {
        Button,
        Column,
        Grid,
        ProgressBar,
        Row,
        Stack,
        Tile,
    } from "carbon-components-svelte";

    type Question = {
        id: number;
        question_id: string;
        question_en: string;
        domain: string;
    };

    type Answer = {
        id: number;
        answer: string;
    };

    const answerScores: Record<string, number> = {
        "strongly-disagree": 0,
        disagree: 1,
        neutral: 2,
        agree: 3,
        "strongly-agree": 4,
    };

    let questions = $state<Question[]>([]);
    let answers = $state<Answer[]>([]);

    $effect(() => {
        const savedQuestions = sessionStorage.getItem("test-questions");
        const savedAnswers = sessionStorage.getItem("test-answers");

        if (savedQuestions) {
            questions = JSON.parse(savedQuestions);
        }

        if (savedAnswers) {
            answers = JSON.parse(savedAnswers);
        }
    });

    const domainScores = $derived.by(() => {
        const scores: Record<string, number> = {
            achiever: 0,
            thinker: 0,
            socialforce: 0,
            creative: 0,
            entrepreneur: 0,
        };

        for (const answer of answers) {
            const question = questions.find((item) => item.id === answer.id);

            if (!question) {
                continue;
            }

            scores[question.domain] += answerScores[answer.answer] ?? 0;
        }

        return scores;
    });

    const highestDomain = $derived.by(() => {
        return Object.entries(domainScores).sort((a, b) => b[1] - a[1])[0];
    });

    const maxScore = $derived.by(() => {
        return Math.max(...Object.values(domainScores));
    });

    function formatDomain(domain: string) {
        return domain.charAt(0).toUpperCase() + domain.slice(1);
    }
</script>

<Grid>
    <Row>
        <Column sm={4} md={4} lg={8}>
            <Stack gap={5}>
                <h1>Your result</h1>

                <Tile>
                    <Stack gap={5}>
                        {#if highestDomain}
                            <h2>{formatDomain(highestDomain[0])}</h2>

                            <p>
                                This is the domain where you scored the highest
                                based on your answers.
                            </p>
                        {:else}
                            <p>No result found yet.</p>
                        {/if}
                    </Stack>
                </Tile>

                <br />
            </Stack>
        </Column>

        <Column sm={4} md={4} lg={8}>
            <Stack gap={5}>
                <h1>Domain scores</h1>

                <Tile>
                    <Stack gap={5}>
                        {#each Object.entries(domainScores) as [domain, score]}
                            <ProgressBar
                                    value={score}
                                    max={maxScore}
                                    labelText={`${formatDomain(domain)} ${score} points`}
                            />
                        {/each}
                    </Stack>
                </Tile>

                <Button
                        href={`${base}/`}
                        kind="primary"
                        style="width: 100%; max-width: 100%;"
                >
                    Back to home
                </Button>
            </Stack>
        </Column>
    </Row>
</Grid>