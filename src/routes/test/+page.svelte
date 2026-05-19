<script lang="ts">
    import { goto } from "$app/navigation";

    import {
        Button,
        ButtonSet,
        Column,
        ExpandableTile,
        Grid,
        ProgressBar,
        RadioTile,
        Row,
        SessionStorage,
        Stack,
        TileGroup,
    } from "carbon-components-svelte";

    import questionsJson from "$lib/data/questions.json";

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

    function shuffleQuestions(questions: Question[]) {
        return [...questions].sort(() => Math.random() - 0.5);
    }

    let currentIndex = $state(0);
    let questions = $state<Question[]>(shuffleQuestions(questionsJson));
    let answers = $state<Answer[]>([]);
    let expanded = $state(false);

    let currentQuestion = $derived(questions[currentIndex]);

    let answer = $derived(
        answers.find((item) => item.id === currentQuestion.id)?.answer ?? ""
    );

    const isFirstQuestion = $derived(currentIndex === 0);
    const isLastQuestion = $derived(currentIndex === questions.length - 1);

    function saveAnswer(value: string) {
        const existingAnswer = answers.find(
            (item) => item.id === currentQuestion.id
        );

        if (existingAnswer) {
            answers = answers.map((item) =>
                item.id === currentQuestion.id
                    ? { id: item.id, answer: value }
                    : item
            );

            return;
        }

        answers = [
            ...answers,
            {
                id: currentQuestion.id,
                answer: value,
            },
        ];
    }

    function previousQuestion() {
        if (currentIndex > 0) {
            currentIndex = currentIndex - 1;
            expanded = false;
        }
    }

    function nextQuestion() {
        if (!answer) {
            return;
        }

        if (isLastQuestion) {
            seeResults();
            return;
        }

        currentIndex = currentIndex + 1;
        expanded = false;
    }

    function seeResults() {
        goto("/result");
    }
</script>

<SessionStorage key="test-current-index" bind:value={currentIndex} />
<SessionStorage key="test-questions" bind:value={questions} />
<SessionStorage key="test-answers" bind:value={answers} />

<Grid>
    <Stack gap={5}>
        <Row>
            <Column>
                <h1>
                    Question {currentIndex + 1} of {questions.length}
                </h1>
            </Column>
        </Row>

        <Row>
            <Column>
                <ProgressBar
                        value={currentIndex + 1}
                        max={questions.length}
                />

                <br />
            </Column>
        </Row>

        <Row>
            <Column>
                <ExpandableTile
                        bind:expanded
                        tileCollapsedLabel="Bahasa Indonesia"
                >
                    <div slot="above" style="height: 15rem">
                        <h2>{currentQuestion.question_en}</h2>
                    </div>

                    <div slot="below">
                        <p>{currentQuestion.question_id}</p>
                    </div>
                </ExpandableTile>

                <br />
            </Column>

            <Column>
                <TileGroup
                        legendText="Choose your answer"
                        name={`answer-${currentQuestion.id}`}
                        selected={answer}
                        on:select={(event) => saveAnswer(event.detail)}
                >
                    <RadioTile value="strongly-agree">
                        Strongly agree
                    </RadioTile>

                    <RadioTile value="agree">
                        Agree
                    </RadioTile>

                    <RadioTile value="neutral">
                        Neutral
                    </RadioTile>

                    <RadioTile value="disagree">
                        Disagree
                    </RadioTile>

                    <RadioTile value="strongly-disagree">
                        Strongly disagree
                    </RadioTile>
                </TileGroup>

                {#if isFirstQuestion}
                    <Button
                            kind="primary"
                            style="width: 100%; max-width: 100%; margin-top: 1rem;"
                            disabled={!answer}
                            on:click={nextQuestion}
                    >
                        Next
                    </Button>

                {:else}
                    <ButtonSet style="width: 100%;">
                        <Button
                                kind="secondary"
                                style="width: 50%; max-width: 100%; margin-top: 1rem;"
                                on:click={previousQuestion}
                        >
                            Previous
                        </Button>

                        <Button
                                kind="primary"
                                style="width: 50%; max-width: 100%; margin-top: 1rem;"
                                disabled={!answer}
                                on:click={nextQuestion}
                        >
                            {#if isLastQuestion}
                                Results
                            {:else}
                                Next
                            {/if}
                        </Button>
                    </ButtonSet>
                {/if}
            </Column>
        </Row>
    </Stack>
</Grid>