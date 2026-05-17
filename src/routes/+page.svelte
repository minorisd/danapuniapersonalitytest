<script>
    import {
        Button,
        Column,
        Grid,
        Row,
        Tag, Theme,
        Tile,
    } from "carbon-components-svelte";
</script>
<Grid>
    <Row>
        <Column lg={6}>
            <Tile>
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
            </Tile>
            <Button href="/test" kind="primary">
                Start test
            </Button>
        </Column>
    </Row>
</Grid>

<style>
    p {
        margin-top: 1rem;
        line-height: 1.6;
    }

    .tags {
        display: flex;
        flex-wrap: wrap;
        gap: 0.5rem;
        margin-top: 1rem;
    }

    :global(.bx--btn) {
        width: 100%;
        max-width: 100%;
        margin-top: 1.5rem;
    }
</style>