<!DOCTYPE html>
<!-- svelte-ignore a11y-missing-attribute -->
<html>
  <head>
    <meta charset="utf-8">
    <style>
      #okno {
        width: 1000px;
        height: 500px;
        text-align: center;
        padding: 15px;
        border: 3px solid #1C64F2;
        background-color: #FDFEFE;
        border-radius: 10px;
        color: #17202A;
        display: none;
        position: fixed;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        margin: auto;
      }
      #okno:target {display: block;}
      .close {
        display: inline-block;
        border: 1px solid #0000cc;
        color: #0000cc;
        padding: 0 12px;
        margin: 10px;
        text-decoration: none;
        background: #f2f2f2;
        font-size: 14pt;
      }

      #okno1 {
        width: 1000px;
        height: 500px;
        text-align: center;
        padding: 15px;
        border: 3px solid #1C64F2;
        background-color: #FDFEFE;
        border-radius: 10px;
        color: #17202A;
        display: none;
        position: fixed;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        margin: auto;
      }
      #okno1:target {display: block;}
      .close {
        display: inline-block;
        border: 1px solid #0000cc;
        color: #0000cc;
        padding: 0 12px;
        margin: 400px;
        text-decoration: none;
        background: #f2f2f2;
        font-size: 14pt;
        cursor:pointer;
      }

      #okno2 {
        width: 1000px;
        height: 500px;
        text-align: center;
        padding: 15px;
        border: 3px solid #1C64F2;
        background-color: #FDFEFE;
        border-radius: 10px;
        color: #17202A;
        display: none;
        position: fixed;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        margin: auto;
      }
      #okno2:target {display: block;}
      .close {
        display: inline-block;
        border: 1px solid #0000cc;
        color: #0000cc;
        padding: 0 12px;
        margin: 400px;
        text-decoration: none;
        background: #f2f2f2;
        font-size: 14pt;
        cursor:pointer;
      }

      #okno3 {
        width: 1000px;
        height: 500px;
        text-align: center;
        padding: 15px;
        border: 3px solid #1C64F2;
        background-color: #FDFEFE;
        border-radius: 10px;
        color: #17202A;
        display: none;
        position: fixed;
        top: 0;
        right: 0;
        bottom: 0;
        left: 0;
        margin: auto;
      }
      #okno3:target {display: block;}
      .close {
        display: inline-block;
        border: 1px solid #0000cc;
        color: #0000cc;
        padding: 0 12px;
        margin: 400px;
        text-decoration: none;
        background: #f2f2f2;
        font-size: 14pt;
        cursor:pointer;
      }
      .close:hover {background: #FDFEFE;}
    </style>
  </head>
 
  <body>
   
    <div id="okno">
      Зарегистрировать объект<br>
      <a href="#" class="close">X</a>
    </div>

    <div id="okno1">
        Поиск услуг<br>
        <a href="#" class="close">X</a>
      </div>

    <div id="okno2">
        Отслеживание объектов недвижимости<br>
        <a href="#" class="close">X</a>
      </div>

    <div id="okno3">
        Остались вопросы?<br>
        <a href="#" class="close">X</a>
      </div>

     
    <center>
    
        <h1 style="color:#17202A text-xl">Справка</h1> 
        
        <a href="#okno" class="flex flex-col items-center bg-white border border-gray-200 rounded-lg shadow md:flex-row md:max-w-xl hover:bg-gray-100 dark:border-gray-700 dark:bg-gray-800 dark:hover:bg-gray-700">
            <img class="object-cover w-full rounded-t-lg h-382 md:h-auto md:w-96 md:rounded-none md:rounded-l-lg" src="https://cmunhoz.com.br/wp-content/uploads/2020/01/Documentação-para-loteamento-saiba-mais-sobre-o-Habite-se-1.jpg" alt="">
            <div class="flex flex-col justify-between p-4 leading-normal">
                <h5 class="mb-5 font-bold tracking-tight text-gray-900 dark:text-white">Зарегистрировать объект</h5>
                <p class="mb-3 font-normal text-gray-700 dark:text-gray-400">Тут будет написан очень заманчивый текст.</p>
            </div>
        </a>
    
        <a href="#okno1" class="flex flex-col items-center bg-white border border-gray-200 rounded-lg shadow md:flex-row md:max-w-xl hover:bg-gray-100 dark:border-gray-700 dark:bg-gray-800 dark:hover:bg-gray-700">
            <div class="flex flex-col justify-between p-4 leading-normal">
                <h5 class="mb-5 font-bold tracking-tight text-gray-900 dark:text-white">Поиск услуг</h5>
                <p class="mb-3 font-normal text-gray-700 dark:text-gray-400">Тут будет написан еще более заманчивый текст.</p>
            </div>
            <img class="object-cover w-full rounded-t-lg h-382 md:h-auto md:w-96 md:rounded-none md:rounded-l-lg" src="https://www.navicosoft.com/wp-content/uploads/2022/01/60bf5359444365d8260b929d_banking-customer-centric.png" alt="">
        </a>
    
        <a href="#okno2" class="flex flex-col items-center bg-white border border-gray-200 rounded-lg shadow md:flex-row md:max-w-xl hover:bg-gray-100 dark:border-gray-700 dark:bg-gray-800 dark:hover:bg-gray-700">
            <img class="object-cover w-full rounded-t-lg h-382 md:h-auto md:w-96 md:rounded-none md:rounded-l-lg" src="https://ilinsk.ru/upload/iblock/aa3/aa3ddedff7879927f2734483569e4dec.jpg" alt="">
            <div class="flex flex-col justify-between p-4 leading-normal">
                <h5 class="mb-5 font-bold tracking-tight text-gray-900 dark:text-white">Отслеживание объектов недвижимости</h5>
                <p class="mb-3 font-normal text-gray-700 dark:text-gray-400">Тут будет написан слишком заманчивый текст.</p>
            </div>
        </a>
    
        <a href="#okno3" class="flex flex-col items-center bg-white border border-gray-200 rounded-lg shadow md:flex-row md:max-w-xl hover:bg-gray-100 dark:border-gray-700 dark:bg-gray-800 dark:hover:bg-gray-700">
            <div class="flex flex-col justify-between p-4 leading-normal">
                <h5 class="mb-5 font-bold tracking-tight text-gray-900 dark:text-white">Остались вопросы?</h5>
                <p class="mb-3 font-normal text-gray-700 dark:text-gray-400">Свяжитесь с нами в любом из предоставленных мессенджерах.</p>
            </div>
            <img class="object-cover w-full rounded-t-lg h-382 md:h-auto md:w-96 md:rounded-none md:rounded-l-lg" src="https://quietest.ru/images/pages/kontakti/kontakti.jpg" alt="">
        </a>
    
        <body>
            
        </body>
    
    </center>
  </body>
</html>


<style>
    h1 {
        margin-block-start: 20px;
        margin-block-end: 32px;
    }

    a {
        margin-block-end: 42px;
    }
</style>