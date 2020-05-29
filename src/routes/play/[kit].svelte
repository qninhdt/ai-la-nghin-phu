<script context="module">
	export function preload(page, session) {
		return { kit: page.params.kit };
	}
</script>

<script>
    import QuestionMenu from "../../components/QuestionMenu";
    import { goto } from '@sapper/app'
    import { onMount } from "svelte"

    export let kit

    let questions, active, active_index, answer, correct, image
    let hide_modal = true

    let text = {
        correct: [
            "Không làm đc thì ... :I",
            "Câu dễ ~",
            "Qua mốc 1",
            "Tạm",
            "Tiếp đi",
            "Qua mốc 2",
            "Nice !",
            "Tuyệt !",
            "Qua mốc 3 o_o",
            "Gần thắng",
            "Game là dễ"
        ],
    }

    let helps = {
        friend: true,
        half: true
    }
    
    async function loadData() {
        questions = await import(`../../data/kit_${kit}.js`)
        active = questions[0]
        active_index = 0;
    }

    function choose(i) {
        answer = i
    }

    function check() {
        if (answer == null) return;

        correct = answer == active.correct
        // correct = true
        
        image = "/images/correct-" + active_index + ".svg"
        
        const modal = jQuery("#game-modal")
        
        modal.modal({
            showClose: false,
            fadeDuration: 100
        })
    }

    onMount(() => {
        jQuery("#game-modal").on('modal:after-close', () => {
            if (correct) {
                active_index += 1;
                active = questions[active_index]
                answer = null
            } else {
                goto("/gameover")
            }
        })
    })

    loadData()

    function friend() {
        helps.friend = false
    }

    function half() {
        switch (active.correct) {
            case 0:
                active.answers[2] = ""
                active.answers[3] = ""
                break;
            case 1:
                active.answers[0] = ""
                active.answers[3] = ""
                break;
            case 2:
                active.answers[1] = ""
                active.answers[3] = ""
                break;
            case 3:
                active.answers[0] = ""
                active.answers[2] = ""
                break;
        }
        helps.half = false
    }

</script>

<style>
    #question-menu {
        margin-left: 50px;
    }
    #game-question {
        background: #f5f5f5;
        border-left: 5px solid #00d1b2;
    }
    .game-answers button {
        outline: none;
        text-align: center;
        margin: 10px;
        padding: 30px 0px;
        border: 3px solid #00d1b2;
        font-size: 16px;
    }

    .game-answers button.active {
		background: #00d1b2;
		color: white;
        font-weight: 700;
    }

    .game-answers b {
        color: #006152;
    }
    
    #game-modal h2 {
        font-size: larger;
        margin: 30px;
    }

    .helps {
        margin-right: 30px;
    }

    .helps figure {
        border: 2px solid #00d1b2;
        border-radius: 100px;
        margin-bottom: 20px;
        overflow: hidden; 
    }

    .disable {
        pointer-events: none;
        opacity: 0;
    }
    
</style>

<!-- modal -->
<div id="game-modal" class="modal">
    {#if correct != undefined}
        {#if correct}
            <h2><b>#</b> {text.correct[active_index]}</h2>
            <figure class="image is-128x128" style="margin: auto; margin-bottom: 30px">
                <img src={image} alt="Success">
            </figure>
        {:else}
            <h2><b>#</b> SAI</h2>
            <figure class="image is-128x128" style="margin: auto; margin-bottom: 30px">
                <img src="images/wrong.svg" alt="Wrong">
            </figure>
            <h3 style="text-align: center">Đáp án đúng</h3>
            <h4><b>{["A", "B", "C", "D"][active.correct]}.</b> {active.answers[active.correct]}</h4>
        {/if}
    {/if}
</div>


{#if questions}

<div id="game" class="columns">

    <div class="helps">
        <figure class="image is-64x64" style="" class:disable={!helps.friend} on:click={friend}>
            <img src="friend.svg" alt="Wrong">
        </figure>
        <figure class="image is-64x64" style="" class:disable={!helps.half} on:click={half}>
            <img src="half.svg" alt="Wrong">
        </figure>
    </div>

    <div class="column">
        <div class="card question">
            <div class="card-image">
                <!-- <figure class="image is-4by3">
                    <img src="https://bulma.io/images/placeholders/1280x960.png" alt="Placeholder">
                </figure> -->
            </div>
            <div id="game-question" class="card-content">
                <div class="content">{@html active.content}</div>
            </div>
            <div style="padding: 80px; padding-left: 50px;">
                <div class="columns game-answers">
                    <button class="column is-6" on:click={() => choose(0)} class:active={answer == 0} ><b>A.</b> {@html active.answers[0]}</button>
                    <button class="column is-6" on:click={() => choose(1)} class:active={answer == 1} ><b>B.</b> {@html active.answers[1]}</button>
                </div>
                <div class="columns game-answers" >
                    <button class="column is-6" on:click={() => choose(2)} class:active={answer == 2} ><b>C.</b> {@html active.answers[2]}</button>
                    <button class="column is-6" on:click={() => choose(3)} class:active={answer == 3} ><b>D.</b> {@html active.answers[3]}</button>
                </div>
            </div>
        </div>   
        <button on:click={check} class="button is-primary" style="margin: 30px auto; display:block">Chắc chắn</button>

    </div>
    <div id="question-menu" class="column is-2">
        <QuestionMenu bind:active={active_index}></QuestionMenu>
    </div> 
</div>

{/if}
