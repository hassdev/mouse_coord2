<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8" />
<title>mouse coordinates jq</title>
<style>
	html, body {
		width: 100%;
		height: 100%;
		padding: 0;
		margin: 0;
	}
	body {
		background-color: rgba(100,100,100,0.2);
		overflow: hidden;
	}

	#wrapper {
		width: 100%;
		min-height: 100%;
		margin: 0 auto;
		position: relative;
	}

	#pp {
		width: 100px;
		height: 100px;
		background-color: rgba(100,0,0,0.3);
		position: absolute;
		bottom: 0;
		left: 0;
		right: 0;
		margin: 0 auto;
	}

	svg {
		outline: 1px solid blue;
		position: absolute;
		bottom: 0;
		left: 0;
		right: 0;
		margin: 0 auto;
		width: 100%;
		height: 100%;
	}
</style>
</head>

<body>
	<div id="wrapper" onmousemove="coords(event)" onmouseout="clear_status()">
		<div id="status"></div>
		<div id="pp"></div>
		<div id="status2"></div>

		<svg id="mysvg" height="400" width="450"></svg>
	</div><!--/#wrapper-->
	<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
	<script>
		function coords(e) {
			//viewport size
			var svgw = $("svg").width();
			var svgh = $("svg").height();

			//mouse coordinates
			var mx = e.clientX;
			var my = e.clientY;

			//coords in percentage relative to viewport
			var xper = (mx/svgw)*100;
			var yper = (my/svgh)*100;

			//coords in decimal relative to viewport
			var xdec = (mx/svgw);
			var ydec = (my/svgh);

			//midpoint
			var mdpt = svgw/2;

			//y-initial
			var yini = svgh - 100;

			//random number
			var rand = {
				aa: Math.floor(Math.random()*15),
				ba: Math.floor(Math.random()*15),
				ca: Math.floor(Math.random()*15),
				da: Math.floor(Math.random()*15),
				ea: Math.floor(Math.random()*15),
				fa: Math.floor(Math.random()*15),
				ga: Math.floor(Math.random()*15),
				ha: Math.floor(Math.random()*15),
				ia: Math.floor(Math.random()*15),
				ja: Math.floor(Math.random()*15),
				ka: Math.floor(Math.random()*15),
				la: Math.floor(Math.random()*15),
				ma: Math.floor(Math.random()*15),
				na: Math.floor(Math.random()*15),
				oa: Math.floor(Math.random()*15),
				pa: Math.floor(Math.random()*15),
				qa: Math.floor(Math.random()*15),
				ra: Math.floor(Math.random()*15),
				sa: Math.floor(Math.random()*15),
				ta: Math.floor(Math.random()*15),
				ua: Math.floor(Math.random()*15),
				va: Math.floor(Math.random()*15),
				wa: Math.floor(Math.random()*15),
				xa: Math.floor(Math.random()*15),
				ya: Math.floor(Math.random()*15),
				za: Math.floor(Math.random()*15)
			};


			//reversed
			var mxr = mx - mdpt;
			var mxr = -mxr;

			var mxptr = {
				mx1: -((mx-mdpt)/5),
				mx2: -((mx-mdpt)/4),
				mx3: -((mx-mdpt)/3),
				mx4: -((mx-mdpt)/2),
				mx5: -(((mx-mdpt)/3)*2),
				mx6: -(((mx-mdpt)/4)*3),
				mx7: -(((mx-mdpt)/5)*4)
			};

			if(mxptr.mx1 <= mdpt) {
				mxptr.mx1 = -(mdpt*0.1);
				mxptr.mx2 = -(mdpt*0.2);
				mxptr.mx3 = -(mdpt*0.3);
				mxptr.mx4 = -(mdpt*0.4);
				mxptr.mx5 = -(mdpt*0.5);
				mxptr.mx6 = -(mdpt*0.6);
				mxptr.mx7 = -(mdpt*0.7);
			}

			//mx path points
			var mxpt = {
				mx1: (((mx-mdpt)/5))+mdpt,
				mx2: (((mx-mdpt)/4))+mdpt,
				mx3: ((mx-mdpt)/3)+mdpt,
				mx4: ((mx-mdpt)/2)+mdpt,
				mx5: (((mx-mdpt)/3)*2)+mdpt,
				mx6: (((mx-mdpt)/4)*3)+mdpt,
				mx7: (((mx-mdpt)/5)*4)+mdpt
			};

			if(mxpt.mx1 <= mdpt) {
				mxpt.mx1 = mdpt*1;
				mxpt.mx2 = mdpt*1.05;
				mxpt.mx3 = mdpt*1.08;
				mxpt.mx4 = mdpt*1.1;
				mxpt.mx5 = mdpt*1.13;
				mxpt.mx6 = mdpt*1.15;
				mxpt.mx7 = mdpt*1.18;
			}

			if (mx <= mdpt*1.5) {
				mx = mdpt*1.4;
				mxr = -(mdpt*0.3);
			}

			$("#status").html("Viewport width: " + svgw + "<br>Viewport height: " + svgh + "<br><br>X coords: " + mx + "<br>Y coords: " + my + 
							  "<br><br>X(%): " + xper + "<br><br>Y(%): " + yper + "<br><br>X(decimal): " + xdec + "<br><br>Y(decimal):" + ydec + 
							  "<br><br>mid point: " + mdpt + "<br>mxr: " + (-mxr) + "<br><br>mxpt.mx1: " + mxpt.mx1 + "<br><br>mxptr.m1: " + mxptr.mx1 + 
							  "<br>mxptr.mx2: " + mxptr.mx2 + "<br>mxptr.mx3: " + mxptr.mx3 + "<br>mxptr.mx4: " + mxptr.mx4 + "<br>mxptr.mx5: " + mxptr.mx5 +
							  "<br>mxptr.mx6: " + mxptr.mx6 + "<br>mxptr.mx7: " + mxptr.mx7);


			//$("#mysvg").html('<path d="M 284 184 Q 304 154,324 184 T 364 184" stroke="orange" stroke-width="7" fill="none" />');
			/*$("#mysvg").html('<path d="M ' + mdpt + ' ' + yini + 
				                     ' Q ' + (hpos*1.1) + ' ' + (yini-rand.aa) + ','
				                     	   + (hpos*1.2) + ' ' + (yini+rand.ba) + 
				                     ' T ' + (hpos*1.4) + ' ' + (yini-rand.ca) + 
				                     ' Q ' + (hpos+1.5) + ' ' + (yini+rand.da) + ','
				                     	   + (hpos*1.6) + ' ' + (yini-rand.ea) + 
				                     ' T ' + (hpos*1.8) + ' ' + (yini+rand.fa) + 
				                     ' Q ' + (hpos*1.9) + ' ' + (yini-rand.ga) + ','
				                     	   + (hpos*2.0) + ' ' + (yini+rand.ha) + 
				                     ' T ' + (mx) + ' ' + (yini-rand.ia) + 
				                     '" stroke="orange" stroke-width="7" fill="none" />');*/
			var input1 = '<path d="M ' + mdpt + ' ' + yini + 
									 ' L ' + mxpt.mx1 + ' ' + (yini+rand.aa) + ','
									       + mxpt.mx2 + ' ' + (yini-rand.ba) + ','
									       + mxpt.mx3 + ' ' + (yini+rand.ca) + ','
									       + mxpt.mx4 + ' ' + (yini-rand.da) + ','
									       + mxpt.mx5 + ' ' + (yini+rand.ea) + ','
									       + mxpt.mx6 + ' ' + (yini-rand.fa) + ','
									       + mxpt.mx7 + ' ' + (yini+rand.ga) + ','
									       + (mx) + ' ' + (yini-rand.fa) +
									 '" stroke="orange" stroke-width="7" stroke-linejoin="round" fill="none" />';

			var input2 = '<path d="M ' + (mdpt+50) + ' ' + (yini+20) + 
									 ' L ' + (mxpt.mx1+50) + ' ' + ((yini+50)-rand.ha) + ','
									       + (mxpt.mx2+50) + ' ' + ((yini+50)+rand.ia) + ','
									       + (mxpt.mx3+50) + ' ' + ((yini+50)-rand.ja) + ','
									       + (mxpt.mx4+50) + ' ' + ((yini+50)+rand.ka) + ','
									       + (mxpt.mx5+50) + ' ' + ((yini+50)-rand.la) + ','
									       + (mxpt.mx6+50) + ' ' + ((yini+50)+rand.ma) + ','
									       + (mxpt.mx7+50) + ' ' + ((yini+50)-rand.na) + ','
									       + (mx) + ' ' + ((yini+50)+rand.oa) +
									 '" stroke="orange" stroke-width="7" stroke-linejoin="round" fill="none" />';

			var input3 = '<path d="M ' + mdpt + ' ' + yini + 
									 ' l ' + mxptr.mx1 + ' ' + (0+rand.oa) + ','
									       + (mxptr.mx2-mxptr.mx1) + ' ' + (-20+rand.pa) + ','
									       + (mxr-mxptr.mx1-(mxptr.mx2-mxptr.mx1)) + ' ' + 0 +
									 '" stroke="red" stroke-width="7" fill="none" />';

			$("#mysvg").html(input1+input2+input3);
		}

		function clear_status() {
			$("#status").html("X coords: " + 0 + "<br>Y coords: " + 0);
		}
	</script>
</body>
</html>
