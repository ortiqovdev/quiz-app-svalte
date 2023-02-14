<script lang="ts">
    type Variant = {
        text: string;
        isRight: boolean;
    };

    type Question = {
        title: string;
        content: string;
        variants: Variant[];
        selected: number
    };

    const questions: Question[] = [
        {
            title: "What about Javascript?",
            content:
                "Lorem ipsum dolor sit amet consectetur adipisicing elit. Recusandae reiciendis facere deleniti. Dolorem facere laborum eum assumenda aut earum laudantium nam, corporis reprehenderit ea repudiandae at nesciunt eos sapiente iste?",
            variants: [
                {
                    text: "Javscript is Programming Language",
                    isRight: true,
                },
                {
                    text: "Javascript is Markup Language",
                    isRight: false,
                },
                {
                    text: "Javascript is CSS Preprocessor",
                    isRight: false,
                },
                {
                    text: "Javascript is binary format",
                    isRight: false,
                },
            ],
            selected: -1
        },
        {
            title: "What about Javascript 2?",
            content:
                " 2 Lorem ipsum dolor sit amet consectetur adipisicing elit. Recusandae reiciendis facere deleniti. Dolorem facere laborum eum assumenda aut earum laudantium nam, corporis reprehenderit ea repudiandae at nesciunt eos sapiente iste?",
            variants: [
                {
                    text: "Javscript is Programming Language 2",
                    isRight: false,
                },
                {
                    text: "Javascript is Markup Language 2",
                    isRight: false,
                },
                {
                    text: "HTML is CSS Preprocessor 2",
                    isRight: true,
                },
                {
                    text: "Javascript is binary format 2",
                    isRight: false,
                },
            ],
            selected: -1
        },
        {
            title: "What about Javascript 3?",
            content:
                " 3 Lorem ipsum dolor sit amet consectetur adipisicing elit. Recusandae reiciendis facere deleniti. Dolorem facere laborum eum assumenda aut earum laudantium nam, corporis reprehenderit ea repudiandae at nesciunt eos sapiente iste?",
            variants: [
                {
                    text: "HTML is Programming Language 3",
                    isRight: false,
                },
                {
                    text: "Javascript is Markup Language 3",
                    isRight: false,
                },
                {
                    text: "SCSS is CSS Preprocessor",
                    isRight: true,
                },
                {
                    text: "HTML is binary format",
                    isRight: false,
                },
            ],
            selected: -1
        },
    ];

    let current: number = 0

    let question: Question = questions[current]

    let selectedIndex: number = question.selected;

    function select(index: number) {
        selectedIndex = index;
        question.selected = index
    }

    function next(offset: number) {
        let c = current +  offset

        if (c < 0) {
            c = questions.length - 1
        }
        else if (c >= questions.length) {
            c = 0
        }
        current = c
        question = questions[current]
        selectedIndex = question.selected
    }
</script>

<main>
    <h1>Quizz</h1>

    <p class="indicator">
        <button on:click={ () => next(-1) }> {'<'} </button>
        Question {current + 1} of {questions.length}
        <button on:click={ () => next(1) }> {'>'} </button>
    </p>

    <h3 class="title">{question.title}</h3>
    <p class="content">
        {question.content}
    </p>

    <ol type="A" class="answers">
        {#each question.variants as variant, index}
            <!-- svelte-ignore a11y-click-events-have-key-events -->
            <li
                on:click={() => select(index)}
                class={index != selectedIndex
                    ? "variant"
                    : variant.isRight
                    ? "variant success"
                    : "variant error"}
            >
                {variant.text}
            </li>
        {/each}
    </ol>
</main>

<style>
    main {
        padding: 50px;
        width: 60%;
        margin: 0 auto;
    }

    h1 {
        margin: 20px 0;
    }

    .indicator {
        text-align: center;
        padding: 10px;
    }

    .title {
        margin: 20px 0;
    }

    .answers {
        display: grid;
        margin-top: 20px;
        grid-template-columns: 1fr 1fr;
        gap: 20px;
    }

    .variant {
        padding: 5px;
        border: 1px solid #bfbfbf;
        border-radius: 5px;
        transition: all 200ms 0s ease;
    }

    .variant.success {
        background-color: green;
        color: white;
    }

    .variant.error {
        background-color: red;
        color: white;
    }

    .variant:hover {
        background-color: #eaeaea;
        cursor: pointer;
    }

    .variant:active {
        background-color: #d9d9d9;
    }
</style>
