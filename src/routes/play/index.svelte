<style>
    #game-select {
        text-align: center;
        padding-top: 50px;
    }
    #game-select .card {
        margin: 20px;
    }
    .select-image {
        position: relative;
    }
    .select-image:before {
        content: "";
        z-index: 10;
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 255, 255, 0.3);
        transition-duration: 1s;
    }
    .select-image:hover:before {
        opacity: 0;
    }
</style>

<div id="game-select" class="container">
    <h1 class="title">Chọn mức chơi</h1>

    <div class="columns">
        <!-- NOOB -->
        <div class="column card">
            <div class="card-image select-image">
                <figure class="image is-4by3">
                    <img src="noob.png" alt="Placeholder">
                </figure>
            </div>
            <div class="card-content">
                <div class="title"># Noob</div>
                <p class="subtitle">
                    Có các cột mốc thưởng
                </p>
                <a href="/play/q" class="button is-info is-light">Tôi gà :((</a>
            </div>
        </div>
        <!-- PRO -->
        <div class="column card">
            <div class="card-image select-image">
                <figure class="image is-4by3">
                    <img src="pro.png" alt="Placeholder">
                </figure>
            </div>
            <div class="card-content">
                <div class="title"># Prồ</div>
                <p class="subtitle">
                    Chơi đến câu cuối cùng
                </p>
         
                <a href="/play/q" class="button is-danger is-light">Tuổi ?</a>
            </div>
        </div>
    </div>
</div>