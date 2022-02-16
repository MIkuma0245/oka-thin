# oka-thin
マイスターのために開発
<!DOCTYPE html>
<html>
  <head>
    <meta name="description" content="書籍「動くWebデザインアイディア帳」のサンプルサイトです" />
    <meta name="viewport" content="width=device-width,initial-scale=1.0" />
    <meta charset="UTF-8" />
    <title>ESP32 RGB LED controller</title>
    <link rel="icon" href="data:," />
    <link
      rel="stylesheet"
      type="text/css"
      href="https://coco-factory.jp/ugokuweb/wp-content/themes/ugokuweb/data/reset.css"
    />
    <link rel="stylesheet" type="text/css" href="https://cdn.jsdelivr.net/npm/slick-carousel@1.8.1/slick/slick.css" />
    <link
      rel="stylesheet"
      type="text/css"
      href="https://coco-factory.jp/ugokuweb/wp-content/themes/ugokuweb/data/6-1-7/css/6-1-7.css"
    />
    <style>
    body {text-align: center;display: flex;font-family: 'Trebuchet MS', Arial;flex-direction: column;justify-content: center;align-items: center;}
    nav{
  width: 100%;
  height: 80px;
  background-color: #55acee;
  padding-top: 20px;
  box-sizing: border-box;
  font-size: 30px;
}
ul{display: flex;}
li{list-style: none;}
a{display: block;text-decoration: none;color: white;margin-right: 35px;}
a:hover{color: rgb(214, 1, 1);}

              h1 {color: #55acee;font-family: cursive;font-weight: bold;font-size: 140px;margin-top: 50px;}

              .text-input {position: relative;margin-top: 50px;}

              input[type='time'] {display: inline-block;width: 500px;height: 50px;box-sizing: border-box;outline: none;border: 1px solid lightgray;border-radius: 3px;padding: 10px 10px 10px 100px;
              transition: all 0.1s ease-out;}

              input[type='time'] + label {
                position: absolute;
                top: 0;
                left: 0;
                bottom: 0;
                height: 50px;
                line-height: 50px;
                color: white;
                border-radius: 3px 0 0 3px;
                padding: 0 20px;
                background: #e03616;
                transform: translateZ(0) translateX(0);
                transition: all 0.3s ease-in;
                transition-delay: 0.2s;
              }

              input[type='time']:focus + label {
                transform: translateY(-120%) translateX(0%);
                border-radius: 3px;
                transition: all 0.1s ease-out;
              }

              input[type='time']:focus {
                padding: 10px;
                transition: all 0.3s ease-out;
                transition-delay: 0.2s;
              }
            
              #servoPosR {
                color: red;
                font-size: 30px;
              }
              #servoPosG {
                color: green;
                font-size: 30px;
              }
              #servoPosB {
                color: blue;
                font-size: 30px;
              }
              .slider {
                width: 300px;
              }
              #wrap::before,
              #wrap::after {
                position: fixed;
                z-index: 1;
                top: -15%;
                display: block;
                visibility: hidden;
                width: 50%;
                height: 130%;
                content: '';
                background-color: #fffacd;
              }
              #wrap::before {
                left: 0;
                animation: curtain_l 3s;
                　-webkit-animation: curtain_l 3s;
              }
              #wrap::after {
                right: 0;
                animation: curtain_r 3s;
                　-webkit-animation: curtain_r 3s;
              }

              @keyframes curtain_l {
                0% {
                  visibility: visible;
                }
                20% {
                  transform: rotate(0deg) translateX(0%);
                  background-color: #ff7f50;
                }
                60% {
                  transform: rotate(6deg) translateX(-50%);
                }
                80% {
                  opacity: 1;
                }
                100% {
                  transform: rotate(0deg) translateX(-100%);
                  opacity: 0;
                  visibility: hidden;
                }
              }
              @-webkit-keyframes curtain_l {
                0% {
                  visibility: visible;
                }
                20% {
                  -webkit-transform: rotate(0deg) translateX(0%);
                  background-color: #fffacd;
                }
                60% {
                  -webkit-transform: rotate(6deg) translateX(-50%);
                }
                80% {
                  opacity: 1;
                }
                100% {
                  -webkit-transform: rotate(0deg) translateX(-100%);
                  opacity: 0;
                  visibility: hidden;
                }
              }
              @keyframes curtain_r {
                0% {
                  visibility: visible;
                }
                20% {
                  transform: rotate(0deg) translateX(0%);
                  background-color: #ff7f50;
                }
                60% {
                  transform: rotate(-6deg) translateX(50%);
                }
                80% {
                  opacity: 1;
                }
                100% {
                  transform: rotate(0deg) translateX(100%);
                  opacity: 0;
                  visibility: hidden;
                }
              }
              @-webkit-keyframes curtain_r {
                0% {
                  visibility: visible;
                }
                20% {
                  -webkit-transform: rotate(0deg) translateX(0%);
                  background-color: #fffacd;
                }
                60% {
                  -webkit-transform: rotate(-6deg) translateX(50%);
                }
                80% {
                  opacity: 1;
                }
                100% {
                  -webkit-transform: rotate(0deg) translateX(100%);
                  opacity: 0;
                  visibility: hidden;
                }
              }
              .slider {/*横幅94%で左右に余白を持たせて中央寄せ*/
          width:94%;
          margin:0 auto;
      }

      .slider img {
          width:60vw;/*スライダー内の画像を60vwにしてレスポンシブ化*/
          height:auto;
      }

      .slider .slick-slide {
        transform: scale(0.8);/*左右の画像のサイズを80%に*/
        transition: all .5s;/*拡大や透過のアニメーションを0.5秒で行う*/
        opacity: 0.5;/*透過50%*/
      }

      .slider .slick-slide.slick-center{
        transform: scale(1);/*中央の画像のサイズだけ等倍に*/
        opacity: 1;/*透過なし*/
      }


      /*矢印の設定*/

      /*戻る、次へ矢印の位置*/
      .slick-prev,
      .slick-next {
          position: absolute;/*絶対配置にする*/
          top: 42%;
          cursor: pointer;/*マウスカーソルを指マークに*/
          outline: none;/*クリックをしたら出てくる枠線を消す*/
          border-top: 2px solid #666;/*矢印の色*/
          border-right: 2px solid #666;/*矢印の色*/
          height: 15px;
          width: 15px;
      }

      .slick-prev {/*戻る矢印の位置と形状*/
          left: -1.5%;
          transform: rotate(-135deg);
      }

      .slick-next {/*次へ矢印の位置と形状*/
          right: -1.5%;
          transform: rotate(45deg);
      }

      /*ドットナビゲーションの設定*/

      .slick-dots {
          text-align:center;
        margin:20px 0 0 0;
      }

      .slick-dots li {
          display:inline-block;
        margin:0 5px;
      }

      .slick-dots button {
          color: transparent;
          outline: none;
          width:8px;/*ドットボタンのサイズ*/
          height:8px;/*ドットボタンのサイズ*/
          display:block;
          border-radius:50%;
          background:#ccc;/*ドットボタンの色*/
      }

      .slick-dots .slick-active button{
          background:#333;/*ドットボタンの現在地表示の色*/
      }


      /*========= レイアウトのためのCSS ===============*/

      body{
        background:#eee;
      }

      h2,p {
          text-align:center;
          padding:20px;
      }

      ul{
        margin:0;
        padding: 0;
        list-style: none;
      }
    </style>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
  </head>
  <body>
    <nav><ul><li><a href="#">|HOME|</a></li><li><a href="#">|サービス紹介|</a></li><li><a href="#">|最新情報|</a></li><li><a href="#">|ブログ|</a></li><li><a href="#">|お問い合わせ|</a></li></ul></nav>
    <h1>Oka-thin</h1>
    <div id="wrap"></div>

    <p>Brightness of R: <span id="servoPosR"></span></p>
    <div class="text-input">
      <input type="time" class="slider" id="servoSliderR" onchange="servo(this.value,'R')" value="5" />
      <label for="servoSliderR">Name</label>
    </div>

    <p>Brightness of G: <span id="servoPosG"></span></p>
    <div class="text-input">
      <input type="time" class="slider" id="servoSliderG" onchange="servo(this.value,'G')" value="5" />
      <label for="servoSliderG">Name</label>
    </div>

    <p>Brightness of B: <span id="servoPosB"></span></p>
    <div class="text-input">
      <input type="time" class="slider" id="servoSliderB" onchange="servo(this.value,'B')" value="5" />
      <label for="servoSliderB">Name</label>
    </div>

    <br><br><br><br>
    <h2>おかーティンについての製品説明</h2>
    <h3>おかーティンとは、『さわやかな音』と『カーテンの自動開閉による朝日』で<br/>
      母のように優しく目覚めさせるカーテン自動開閉機器です<br/>
      　　　　絶対に次の日遅刻のできない、学生や社会人の方に使っていただくために開発をしました<br/>
      　　　　スマートフォンのアラーム機能だと、無意識のうちにアラームを止めてしまったり、<br/>
      目覚まし時計だと鬱陶しく爽やかな目覚めをすることができていない等<br/>
      　　　　深夜24時にインターネットが制限される問題から、インターネットから無接続の状態でのスムーズな稼働できよう、設計し<br/>
      　　　　1階や、2階などでは通学路から自分たちの部屋を覗かれてしまうなど、プライバシーの問題を解決することができるのではないか<br/>
      　　　　寮生ならではの、視点から考え、から、この製品のアイディアを考えました。<br/>
      <br><br><br><br>
    <ul class="slider">
      <li>
   <img src="https://lh3.googleusercontent.com/ZTuNJZ5K8TN_xV3RoscTOo1aV6_Ql21cPO61Lf7k2IoVCulGrh0XTy_b1CKgGyKWWM82pImhzYsy_C_-LY36ZjL3RfpxxE6T2OPO9KB_ewPHpXxS68JDmbk1ikzPkJFbQT1KKlKt=w600-h315-p-k" /> </a>
      </li>
      <li>
        <img src="https://coco-factory.jp/ugokuweb/wp-content/themes/ugokuweb/data/6-1-7/img/img_02.jpg" alt="" />
      </li>
      <li>
        <img src="https://coco-factory.jp/ugokuweb/wp-content/themes/ugokuweb/data/6-1-7/img/img_03.jpg" alt="" />
      </li>
      <li>
        <img src="https://coco-factory.jp/ugokuweb/wp-content/themes/ugokuweb/data/6-1-7/img/img_04.jpg" alt="" />
      </li>
      <li>
        <img src="https://coco-factory.jp/ugokuweb/wp-content/themes/ugokuweb/data/6-1-7/img/img_05.jpg" alt="" />
      </li>
      <li>
        <img src="https://coco-factory.jp/ugokuweb/wp-content/themes/ugokuweb/data/6-1-7/img/img_06.jpg" alt="" />
      </li>
      <!--/slider-->
    </ul>


      　　　　　


    </h3>
    <script>
      var sliderR = document.getElementById('servoSliderR');
      var servoPR = document.getElementById('servoPosR');
      servoPR.innerHTML = sliderR.value;
      sliderR.oninput = function () {
        sliderR.value = this.value;
        servoPR.innerHTML = this.value;
      };
      var sliderG = document.getElementById('servoSliderG');
      var servoPG = document.getElementById('servoPosG');
      servoPG.innerHTML = sliderG.value;
      sliderG.oninput = function () {
        sliderG.value = this.value;
        servoPG.innerHTML = this.value;
      };
      var sliderB = document.getElementById('servoSliderB');
      var servoPB = document.getElementById('servoPosB');
      servoPB.innerHTML = sliderB.value;
      sliderB.oninput = function () {
        sliderB.value = this.value;
        servoPB.innerHTML = this.value;
      };
      $.ajaxSetup({ timeout: 1000 });
      function servo(pos, color) {
        $.get('/?value' + color + '=' + pos + '&');
        {
          Connection: close;
        }
      }
      if (sliderR>0) {
          alert('1から100の間で入力してください。');
        } 
    </script>
    <script
      src="https://code.jquery.com/jquery-3.4.1.min.js"
      integrity="sha256-CSXorXvZcTkaix6Yvo6HppcZGetbYMGWSFlBw8HfCJo="
      crossorigin="anonymous"
    ></script>
    <script src="https://cdn.jsdelivr.net/npm/slick-carousel@1.8.1/slick/slick.min.js"></script>
    <script src="https://coco-factory.jp/ugokuweb/wp-content/themes/ugokuweb/data/6-1-7/js/6-1-7.js"></script>
  </body>
</html>

