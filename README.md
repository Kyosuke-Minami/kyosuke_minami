# kyosuke_minami<!DOCTYPE html>
<html lang=ja> 
<head>
<meta charset="UTF-8" />
<title>簡易電卓</title>
<style type="text/css">
  button {
    height : 50px;
    width  : 50px;
  }
  button.equal {
    height : 160px;
  }
  button.zero {
    width : 160px;
  }
  div#panel {
    height : 25px;
    width  : 100%;
    border : 1px solid #000000;
    text-align : right;
    padding-right  : 5px;
  }
</style>
<script type="text/JavaScript">
  var panelNumber ="0";
  var svButton ="";
  var svEnzanshi ="";
  var svNumber = 0;
  
  function clPanel() {
    panelNumber = "0";
    svButton = "";
    svEnzanshi = "";
    svNumber = 0;
    document.getElementById( "panel" ).innerText = panelNumber;
  }

  function pushNum(pushNumber) {
    svButton = pushNumber;

    if (panelNumber == "0" ){
      panelNumber = pushNumber;
    }
    else {
      panelNumber += pushNumber;
    }

    document.getElementById( "panel" ).innerText = panelNumber;
  }
  
  function keisan( enzanshi ) {
    var panel = document.getElementById( "panel" );
    var number = parseFloat(panel.innerText);
    var answer = null;

    if ( svEnzanshi == "/" && number == "0" ) {
      alert("ゼロで除算はできません");
      return;
    }
    
    if ( svButton == "+"
      || svButton == "-"
      || svButton == "*"
      || svButton == "/")
    {
      svEnzanshi = enzanshi;
    }else{
      switch (svEnzanshi) {
        case "+":
          answer = svNumber + number;
        break ;

        case "-":
          answer = svNumber - number;
        break ;

        case "*":
          answer = svNumber * number;
        break ;

        case "/":
          answer = svNumber / number;
        break ;
      }

      if (answer != null) {
        panel.innerText = answer;
      }

      panelNumber = "0";
      svButton = enzanshi ;
      svEnzanshi = enzanshi ;
      svNumber = parseFloat(panel.innerText);
    }
    }
</script>
</head>
<body>
<table border="0">
  <tr>
    <td colspan="5"><div id="panel">0</div></td>
  </tr>
  <tr>
    <td><button onclick="pushNum('7')">７</button></td>
    <td><button onclick="pushNum('8')">８</button></td>
    <td><button onclick="pushNum('9')">９</button></td>
    <td><button onclick="keisan('+')">＋</button></td>
    <td><button onclick="clPanel()">Ｃ</button></td>
  </tr>
  <tr>
    <td><button onclick="pushNum('4')">４</button></td>
    <td><button onclick="pushNum('5')">５</button></td>
    <td><button onclick="pushNum('6')">６</button></td>
    <td><button onclick="keisan('-')">－</button></td>
    <td rowspan="3"><button class="equal" onclick="keisan('=')">＝</button></td>
  </tr>
  <tr>
    <td><button onclick="pushNum('1')">１</button></td>
    <td><button onclick="pushNum('2')">２</button></td>
    <td><button onclick="pushNum('3')">３</button></td>
    <td><button onclick="keisan('*')">×</button></td>
  </tr>
  <tr>
    <td colspan="3"><button class="zero" onclick="pushNum('0')">０</button></td>
    <td><button onclick="keisan('/')">÷</button></td>
  </tr>
</table>
</body>
</html>
