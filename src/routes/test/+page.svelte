<script lang="ts">
    import {
        Button,
        ButtonSet,
        Column,
        ExpandableTile,
        Grid,
        ProgressBar,
        RadioTile,
        Row,
        Stack,
        TileGroup,
    } from "carbon-components-svelte";

    import questions from "$lib/data/questions.json";

    let currentIndex = $state(0);
    let answers = $state<{ id: number; answer: string }[]>([]);

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
            existingAnswer.answer = value;
            return;
        }

        answers.push({
            id: currentQuestion.id,
            answer: value,
        });
    }

    function previousQuestion() {
        if (currentIndex > 0) {
            currentIndex--;
        }
    }

    function nextQuestion() {
        if (!answer) {
            return;
        }

        if (currentIndex < questions.length - 1) {
            currentIndex++;
        }
    }

    function seeResults() {
        console.log(answers);
    }
</script>

<Grid>
    <Stack gap={7}>
        <Row>
            <Column>
                <ProgressBar
                        value={currentIndex + 1}
                        max={questions.length}
                />
            </Column>
        </Row>

        <Row>
            <Column>
                <h1>Question {currentIndex + 1} of {questions.length}</h1>

                <br />

                <ExpandableTile tileCollapsedLabel="Bahasa Indonesia">
                    <div slot="above" style="height: 10rem">
                        {currentQuestion.question_en}
                    </div>

                    <div slot="below">
                        {currentQuestion.question_id}
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
                        Next question
                    </Button>
                {:else}
                    <ButtonSet style="width: 100%; margin-top: 1rem;">
                        <Button
                                kind="secondary"
                                style="width: 50%; max-width: 100%;"
                                on:click={previousQuestion}
                        >
                            Previous question
                        </Button>

                        <Button
                                kind="primary"
                                style="width: 50%; max-width: 100%;"
                                disabled={!answer}
                                on:click={nextQuestion}
                        >
                            {#if isLastQuestion}
                                See results
                            {:else}
                                Next question
                            {/if}
                        </Button>
                    </ButtonSet>
                {/if}
            </Column>
        </Row>
    </Stack>
</Grid>