<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <!-- custom css link -->
    <link rel="stylesheet" href="style.css">
</head>

<body>
        <div class="counter-wrapper">
            <div class="counter">
                <h1 class="count" data-target="5000">5 525</h1>
                <p>Кількість опитаних респондентів</p>
            </div>
            <!-- <div class="counter">
                <h1 class="count" data-target="12168">0</h1>
                <p>Вік опитаних респондентів</p>
            </div> -->


        <script src="main.js"></script>
</body>


<!-- const counts = document.querySelectorAll('.count')
const speed = 97

counts.forEach((counter) => {
    function upDate(){
        const target = Number(counter.getAttribute('data-target'))
        const count = Number(counter.innerText)
        const inc = target / speed        
        if(count < target){
            counter.innerText = Math.floor(inc + count) 
            setTimeout(upDate, 15)
        }else{
            counter.innerText = target
        }
    }
    upDate()
}) -->


<style>
    *{
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        transition: 0.2s linear;
        -webkit-transition: 0.2s linear;
        -moz-transition: 0.2s linear;
        -ms-transition: 0.2s linear;
        -o-transition: 0.2s linear;
    }
    html{
        font-size: 62.5%;
        scroll-behavior: smooth;
    }

    body{
        font-family: "Montserrat", sans-serif;
        min-height: 100vh;
    }

    .counter-wrapper{
        background: black;
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        grid-column-gap: 20rem;
        padding: 8rem 9%;
        margin-top: 5rem;
        position: relative;
       
    }
    .counter-wrapper::before{
        position: absolute;
        content: '';
        content: 0;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0,0,0,0.7);
        z-index: 1;
    }
    .counter{ /* лінія знизу */
    text-align: center;   
    color: #ddd;
    z-index: 2;
    position: relative;
    }
    .counter::before{
        position: absolute;
        content: '';
        bottom: -2rem;
        left: 50%;
        width: 20%;
        height: .2rem;
        background:  rgb(188 143 143);
        border-radius: .5rem;
        -webkit-border-radius: .5rem;
        -moz-border-radius: .5rem;
        -ms-border-radius: .5rem;
        -o-border-radius: .5rem;
        transform: translateX(-50%);
        -webkit-transform: translateX(-50%);
        -moz-transform: translateX(-50%);
        -ms-transform: translateX(-50%);
        -o-transform: translateX(-50%);

    }
    .counter .count{
        font-size: 70px;
        margin-bottom: 1rem;    
        font-family: "Montserrat", sans-serif;
    }
    .counter p{
        font-size: 20px;
        font-family: "Montserrat", sans-serif;
        font-weight: 500;
    }
</style>