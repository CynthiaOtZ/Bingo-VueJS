<template>
    <div class="main">

        <nav> <p>Bingo</p></nav>
        <div class="container">
            <div class="containerLeft">
                <div class="containerCard">
                    <p>CPU</p>
                    <div class="card">
                        <div class="number" v-for="item in cpeu" :data-cpeu="item" :id="item">
                            <p>{{ item }}</p>
                        </div>

                    </div>
                </div>
                <div class="containerCard">
                    <p>TÚ</p>
                    <div class="card">
                        <div class="number" v-for="item in user" :data-user="item" :id="item">
                            <p>{{ item }}</p>
                        </div>
                    </div>
                </div>
            </div>
            <div class="containerRigth">
                <div class="containerCard">
                    <button v-on:click="numero()">{{ numeroBoton }}</button>
                </div>
                <div class="containerCard bingo">
                    <div class="number2" v-for="item in aleatorio">
                        <p>{{ item }}</p>
                    </div>
                </div>
            </div>
        </div>

    </div>
</template>

<style>
.main
{
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}

nav 
{
    width: 100%;
    height: 5%;
    background-color: #77CCA4;
    display: flex;
    justify-content: center;
    align-items: center;
    box-sizing: border-box;
}

nav p 
{
    color: #fff;
    font-size: 30px;
    letter-spacing: 3px;
    margin: 0;
}

.container
{
    width: 100%;
    height: 95%;
    display: flex;
    justify-content: center;
    align-items: center;
}

.containerLeft 
{
    width: 60%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}

.containerCard
{
    width: 100%;
    height: 50%;

    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}

.containerCard p 
{
    margin: 0;
}

.bingo 
{
    flex-direction: row;
    flex-wrap: wrap;
    align-items: flex-start;
}

.card 
{
    width: 80%;
    height: 60%;
    border: 1px solid #F0F0D8;
    border-radius: 15px;

    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
}

.number 
{
    width: 70px;
    height: 70px;
    background-color: #77CCA4;
    border-radius: 5px;
    margin: 5px;
    display: flex;
    justify-content: center;
    align-items: center;
}

.number p 
{
    color: #fff;
    margin: 0;
    margin: 10px;
}

.number2 
{
    width: 50px;
    height: 50px;
    background-color: #77CCA4;
    border-radius: 5px;
    margin: 5px;
    display: flex;
    justify-content: center;
    align-items: center;
}

.number2 p 
{
    color: #fff;
    margin: 0;
}
.containerRigth
{
    width: 40%;
    height: 100%;
    background-color: #F0F0D8;
}

button
{
    padding: 15%;
    border-radius: 50%;
    border: none;
    background-color: #77CCA4;
    color: #fff;
    font-size: 50px;
    cursor: pointer;
}




</style>

<script>
export default {

  data: function () {
      return {

        cpeu: [],
        user: [],
        numeroBoton: 0,
        aleatorio: [],
        aleatorioTurno: [],
        min: 1,
        max: 20,
        contadorCPU: 5,
        contadorUSER: 5

      }
    },
    methods:
    {
        coincidencia: function()
        {
            var thisTemporal = this;

             //Código CPU
             thisTemporal.cpeu.forEach((element, index) => {
                if (thisTemporal.numeroBoton == thisTemporal.cpeu[index]) 
                {
                    //document.getElementById(numero).style.backgroundColor = "#F5F5F5";                                         
                    //console.log("data-cpeu='"+ element+"'");
                    var div = document.querySelector('[data-cpeu="'+element+'"]')
                    div.style.backgroundColor = "#F5F5F5";
                    thisTemporal.contadorCPU --;
                    console.log("CPU "+ thisTemporal.contadorCPU);
                }
                
                
              
            });


            thisTemporal.user.forEach((element, index) => {
                if (thisTemporal.numeroBoton == thisTemporal.user[index]) 
                {
                    //console.log(document.querySelector('[data-user="'+index+'"]'));
                    //console.log("data-cpeu='"+ element+"'");
                    var div = document.querySelector('[data-user="'+element+'"]')
                    div.style.backgroundColor = "#F5F5F5";
                    thisTemporal.contadorUSER --;
                    console.log("USER "+ thisTemporal.contadorUSER);                   
                    
                }
                
            });


        },
        numero: function()
        {
            let thisTemporal= this;

            // thisTemporal.aleatorioTurno.push(thisTemporal.getRandomIntInclusive(thisTemporal.min,thisTemporal.max));

            this.numeroBoton = thisTemporal.getRandomIntInclusive(thisTemporal.min,thisTemporal.max);

            if(this.aleatorio.length < 20)
            {
                while(this.aleatorio.includes(this.numeroBoton))
                {
                    console.log("El numero ya habia salido, generar otro");

                    this.numeroBoton = thisTemporal.getRandomIntInclusive(thisTemporal.min,thisTemporal.max);
                    console.log(this.numeroBoton);
                    
                }

                console.log("Al fin salio otro numero");
                this.aleatorio.push(this.numeroBoton);
                this.coincidencia();

                setTimeout(() => {
                    if (thisTemporal.contadorCPU <= 0) {
                    alert("Gano CPU");
                }

                if (thisTemporal.contadorUSER <= 0) {
                    alert("Gano USER");
                }
                }, 500);

                
            }

            

            

        },
        numero2: function()
        {
            console.log("click");
            let thisTemporal = this;
            //var numero = thisTemporal.getRandomIntInclusive(thisTemporal.min,thisTemporal.max);
            thisTemporal.aleatorioTurno.push(thisTemporal.getRandomIntInclusive(thisTemporal.min,thisTemporal.max));        

            thisTemporal.aleatorioTurno.forEach((elements , index) => 
            {
                if (!thisTemporal.aleatorio.includes(elements)) 
                {
                    thisTemporal.numeroBoton = elements;
                    thisTemporal.aleatorio.push(elements);
                    //console.log("Nuevo CPU " +thisTemporal.cpeu);                    
                    thisTemporal.coincidencia();
                }
                else
                {
                    console.log(thisTemporal.aleatorioTurno);
                    let num = thisTemporal.getRandomIntInclusive(thisTemporal.min,thisTemporal.max);
                    thisTemporal.aleatorioTurno.splice(index, 1,  num);
                    thisTemporal.numeroBoton = num;

                    
                }
            });
                      
        },
             
        players: function()
        {
            let thisTemporal = this;
            let cpeuTurno = [];
            let userTurno = [];

            for(let i = 0; i <5; i++)
            {
                cpeuTurno.push(thisTemporal.getRandomIntInclusive(thisTemporal.min,thisTemporal.max));
                userTurno.push(thisTemporal.getRandomIntInclusive(thisTemporal.min,thisTemporal.max));  
            }            
            //Verificar si se repiten los numeros en los array 
            cpeuTurno.forEach((elements , index) => 
            {
                if (!thisTemporal.cpeu.includes(elements)) 
                {
                    thisTemporal.cpeu.push(elements);
                    //console.log("Nuevo CPU " +thisTemporal.cpeu);                    
                }
                else
                {
                    thisTemporal.cpeu.splice(index, 1,thisTemporal.getRandomIntInclusive(thisTemporal.min,thisTemporal.max));                   
                }
            });

            userTurno.forEach((element , index) => 
            {
                if (!thisTemporal.user.includes(element)) {
                    thisTemporal.user.push(element);   
                    //console.log("Nuevo USER " +thisTemporal.user);                           
                }
                else
                {
                    thisTemporal.user.splice(index, 1, thisTemporal.getRandomIntInclusive(thisTemporal.min,thisTemporal.max));                        
                }
            });


        },

        getRandomIntInclusive: function(min, max)
        {
            min = Math.ceil(min);
            max = Math.floor(max);
            return Math.floor(Math.random() * (max - min + 1) + min);
        },

        
    },
    created()
    {
    },
    mounted: function()
    {

        var thisTemporal = this;
        //thisTemporal.getRandomIntInclusive(thisTemporal.min,thisTemporal.max);
        thisTemporal.players();
        


    }

}
</script>