<html>

<head> 

	<title>Oci's Page Thing</title> 

	<script type="text/javascript" src="QuadScripts.js"></script> 

	<style type="text/css"> 
/*David's cool css file for the soft dev class 2016 winter*/

#wrapper {
	width: 1200px;
	margin:auto;
	background-color: rgb(255,255,0);
}

header {
	width: 1000px;
	top: 50px;
	box-shadow: 10px 10px 10px black;
	margin-left: auto;
	margin-right: auto;
	background-color: black;
	text-align: center;
	color: white;
}

#mycanvas {
	margin-left: 400px;
	border-style:dotted;
	border: 20px;
	background-color:lightblue;
}

#coeff {
	margin-top: 40px;
	float: left;
	left: 200px;
	width: 300px;
	position: absolute;
	background-color: rgb(200,200,200);
	padding: 10px;
	border-radius: 20px;

}

#answers {
	margin-left: 40px;
	margin-top: 200px;
	float: left;
	width: 300px;
	background-color: rgb(200,200,200);
	position: absolute;
	padding: 10px;
}


	</style>


	<link rel="stylesheet" type="text/css" href="quadStyles.css">
	<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.11.0/jquery.min.js"></script>

</head>

<body onload="init()"> 
	<div id="wrapper">
		<header>Quad Thing</header>

		<div id="coeff">
			<p class="formInfo">Coefficients go here<br>
				

				a = <input size="10" type="text" id="quadA" value="1"> <br>
				b = <input size="10" type="text" id="linB" value="0"> <br>
				c = <input size="10" type="text" id="constant" value="0"> <br>
				<button onclick="QF()">Submit Values</button></p>
				<button onclick="plotXint()">Plot X Intercept</button></p>
				<button onclick="plotYint()">Plot Y intercept</button></p>
				<button onclick="newGraph()">New Graph</button></p>
				<button onclick="zoomIn()">Zoom In</button></p>
			</div>
			<div id="answers">
				<p class="vertex"></p>
				<span id="dis"></span>
				<span id="root1"></span>
				<span id="root2"></span>

			</div>

			<canvas id="mycanvas"></canvas>
		</div>
		<script type="text/javascript">
//quad scripts
	var a,b,c,w,h,context,k=10;

	function QF() {
	// getting values to do quadratic formula
	a = $("#quadA").val();
	b = $("#linB").val();
	c = $("#constant").val();
	results();
	graphQuad();
	solutions();
	}


	function init(){
		context = document.getElementById("mycanvas");
		context = context.getContext("2d");
		w = mycanvas.width = 600;
		h = mycanvas.height = 400;
		$("#answers").hide();
		grid();
	}

	function plotYint() {
		
		context.beginPath();
		context.arc(w/2,h/2-c*k,3,0,2*Math.PI);
		context.fill();
	}

	function plotXint() {
		
		context.beginPath();
		context.arc(w/2,h/2-x1*h/k,3,0,2*Math.PI);
		context.fill();
	}

	function graphQuad () {
	for (var i = 0; i < w; i++) {
	x = (w/2-i)/k;
	y = c*1+b*x+a*Math.pow(x,2);
	nx =(w/2-(i+1))/k;
	ny = c*1+b*nx+a*Math.pow(nx,2);
	context.lineWidth = 2;
	context.strokeStyle = "Red";
	context.moveTo(w/2+x*k, h/2-y*k);
	context.lineTo(w/2+nx*k, h/2-ny*k);
	context.stroke();
	};
	};

	function solutions() {
	// qudratic formula
	$("#answers").hide();
	$("#answers").fadeIn(1500);
	d = Math.pow(b*1,2)-4*a*c;
	if (d<0) {
		$("#solution1").text("The solutions are imaginary (no x-intercepts).");
	}
	else{
		x1 = -(b*1)/(2*a)+Math.sqrt(d)/(2*a);
		x2 = -(b*1)/(2*a)-Math.sqrt(d)/(2*a);
		$("#solution1").text("x = " + x1);
		$("#solution2").text("x = " + x2);
	}

	}

	function results () {
	// finding vertext and displaying symline and yint results
	vX = -(b*1)/(2*a);
	vY = a*Math.pow(vX,2)+b*vX+c*1;
	D = Math.pow(b,2)-4*a*c;
	x1 = vX + (Math.sqrt(D)/(2*a))
	x2 = vX - (Math.sqrt(D)/(2*a))
	yint = c;
	$(".vertex").text("Vertex is at (" + vX+","+vY+")");
	$("#discriminant").text("The discriminant is " + D);
	$("#root1").text("x1 is " + x1);
	$("#root2").text("x2 is " + x2);

	}

	function grid() {
	//using the direct variation constant k, we make a grid.
	context.lineWidth=2;
	context.strokeStyle="rgba(0,0,0,.4)";
	for (var i=0; i<w/k; i++) {
		context.beginPath();
		context.moveTo(k*(i+1),0);
		context.lineTo(k*(i+1),h);
		context.stroke();
	}
	for (var i=0; i<h/k; i++) {
		context.beginPath();
		context.moveTo(0,k*(i+1));
		context.lineTo(w,k*(i+1));
		context.stroke();
	}
	context.lineWidth=4;
	context.strokeStyle="rgba(0,0,200,.4)";
	context.beginPath();
	context.moveTo(w/2,0);
	context.lineTo(w/2,h);
	context.stroke();
	context.beginPath();
	context.moveTo(0,h/2);
	context.lineTo(w,h/2);
	context.stroke();
	}

	function newGraph() {
		//clearing canvas and answers and drawing grid
		context.clearRect(0,0,w,h);
		$("#answers").hide();
		grid();
			}

function zoomIN() {
	// zoomey zoom zoom
	context.clearRect(0,0,w,h);
	k+=10;
	grid();
	graphQuad();
}

//	function getYint() {
//		$(".vertex").text("Vertex is at ("w/2,h/2-c*h/k,3,0,2*Math.PI")");
//	}
//
//	function getXint() {
//		$(".vertex").text("Vertex is at ("w/2,h/2-x1*h/k,3,0,2*Math.PI")");w/2,h/2-x1*h/k,3,0,2*Math.PI
//	}
		</script>
	</body>

	</html>





