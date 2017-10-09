<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8" />
  <title>Words to LaTeX</title>
  <meta name="description" content="Translate words into LaTeX">
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>
  <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>
  <script>
    $.ajaxSetup({
      crossDomain: true,
      "Access-Control-Allow-Headers": "Content-Type"
    });
  </script>
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" />
  <link rel="stylesheet" href="css/style.css" />
  <script>
    var PARSEGON_KEY = "HackToTheFuture2017"
  </script>
</head>

<body>
  <div class="row container">
    <div class="col-sm-2"></div>
    <div class="col-sm-8">
      <center>
        <div class="jumbotron">
          <h1>Words to LaTeX</h1>
          <p>Pet project to generate pretty equations for notes during class</p>
        </div>
        <div class="result-menu">
          <label>English</label>
          <textarea id="hypothesisDiv" class="form-control" onkeyup='update()' rows='1' , cols='100'></textarea>
          <br>
          <label>LaTeX:</label>
          <div id="LaTeX" style="padding-bottom: 20px">
          </div>
          <script>
            update = function() {
              callAPI(document.getElementById('hypothesisDiv').value)
              var latexInput = document.getElementById('LaTeX').innerHTML;
              var latexCondensed = latexInput.replace(/\s+/g, '');
              var latexSrc = "https://latex.codecogs.com/gif.latex?" + latexCondensed;
              document.getElementById('latex result').src = latexSrc;
              document.getElementById('latex result').title = latexInput;
            }
            callAPI = function(string) {
              obj = {
                apikey: PARSEGON_KEY,
                plaintext: string
              }
              $.ajax({
                url: "http://api.parsegon.com/translate",
                type: "POST",
                async: false,
                'Content-Type': 'application/json',
                data: obj,
                success: function(results) {
                  document.getElementById('LaTeX').innerHTML = results['latex']
                }
              });
            };
          </script>
          <div class="results">
            <img id="latex result" src="https://latex.codecogs.com/gif.latex?dictate&space;\;&space;an&space;\;&space;equation!">
          </div>
      </center>
      </div>
    </div>
    <div class="col-sm-2"></div>
  </div>
</body>
</html>
