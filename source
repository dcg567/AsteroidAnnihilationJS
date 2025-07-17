//-----------------------------------------------------------------------------------------------------------------------------
//HOW TO PLAY

//Once the game loads, there will be a number of things on screen so dont panic. 
//Firstly we have our ship in the centre of the screen, We have some planets orbiting around us, the planets are just for aestethics.
//Around our ship will be a bunch of moving asteroids
//The aim of the game is to destroy all the asteroids before the time runs out
//You will have to manually fly around using: up, down, left, right, q, e (q = inwards movement, e = outwards movement)
//Once you are near an asteroid, press the space bar to destroy it and then move around destroying them all!
//Our game supports web socket functionality, meaning you can play together with your friends
 
 //---------------------------------------------------------------------------------------------------------------------------

//raw code grabbed from my upload on Ancient Brain//

AB.clockTick       = 80;    	// Speed of run: Step every n milliseconds.

AB.maxSteps        = 10000;    	// Length of run: Maximum length of run in steps. Default 1000.

AB.screenshotStep  = 50;   	// Take screenshot on this step. (All resources should have finished loading.) Default 50.
  
 
 const FILE_ARRAY = [ 
        
		"/uploads/dg/earth.png",
		"/uploads/dg/asteroid_1.jpeg",  //planet + asteroid images
		"/uploads/dg/asteroid_4.jpeg",
		"/uploads/dg/asteroid_5.jpeg",
		"/uploads/dg/marmar.jpeg",
		"/uploads/dg/venven.jpeg",
		"/uploads/dg/mermer.jpeg",
		"/uploads/dg/jupii.jpeg",
		"/uploads/dg/satsat.jpeg",
		"/uploads/dg/uraura.jpeg",
		"/uploads/dg/nepnep.jpeg",
		"/uploads/dg/rings.png",
		"/uploads/dg/ringu.png",
		
		
        "/uploads/dg/right.jpg", //skybox images
        "/uploads/dg/left.jpg",
        "/uploads/dg/top.jpg",
        "/uploads/dg/bot.jpg",
        "/uploads/dg/front.jpg",
        "/uploads/dg/back.jpg",
        
        "/uploads/dg/rocket.jpeg",
        "/uploads/dg/boom.jpeg",
		];
	

const SKYCOLOR 	= 0xffffff;	

const ARMYSIZE = 45;
//The amount of asteroids and planets

const objectsize = 225; //size of each asteroid

     
const objectsizeE = 400, objectsizeM = 300, objectsizeV = 350, objectsizeME = 200, objectsizeJ = 900, objectsizeS = 600, objectsizeSR = 600,  objectsizeU = 300, objectsizeUR = 600, objectsizeN = 300, objectsizeSS = 200;
//Size of each planet + rings

const WALKSTEP = 20;  // bounds of the random move per timestep 

const MAXPOS                = 4000 ;            // start things within these bounds                    
const startRadiusConst	 	= MAXPOS * 1.5 ;	// distance from centre to start the camera at
const maxRadiusConst 		= MAXPOS * 5 ;		// maximum distance from camera that will render things  

const skyboxConst			= MAXPOS * 4;      //size of our skybox

ABHandler.MAXCAMERAPOS 		= MAXPOS * 1.25 ;			// allow camera go far away

ABWorld.drawCameraControls 	= false; 

AB.drawRunControls 			= false;

// declaring all the variables
var THEARMY = new Array( ARMYSIZE );	

var textureArray = new Array ( FILE_ARRAY.length );
	
var EARTH, MARS, VENUS, MERCURY, JUPITER, SATURN, SATURNRING, URANUS, URANUSRING, NEPTUNE, SHIP; //declaring our planets

var timer;


var score = 0;

function load_resources()		// asynchronous file loads - call initScene() when all finished 
{
	for ( var i = 0; i < FILE_ARRAY.length; i++ ) 
	  startFileLoad ( i );						// launch n asynchronous file loads

}


	
function startFileLoad ( n )				// asynchronous file load of texture n | from sample
{
	var loader = new THREE.TextureLoader();

	loader.load ( FILE_ARRAY[n], function ( thetexture )  	 
	{
		thetexture.minFilter  = THREE.LinearFilter;
		textureArray[n] = thetexture;
		if ( asynchFinished() ) initArmy();
	
	     
	});	

}
 
function asynchFinished()		// all file loads returned | from sample
{
	for ( var i = 0; i < FILE_ARRAY.length; i++ ) 
		if ( ! textureArray[i] ) 
			return false;
		
	return true;
}


function initArmy()		 // called when all textures ready  //from sample world

{
 var t = 0;

 for ( var c=1 ; c <= ARMYSIZE ; c++ )
 {

    var shape = new THREE.CubeGeometry( objectsize, objectsize, objectsize ); //creates all cubes the size of the declared size
  
  	var theobject  = new THREE.Mesh( shape );

  	theobject.position.x = AB.randomIntAtoB ( -3000, 3000);   	//random postions for the asteroids
  	theobject.position.z = AB.randomIntAtoB ( -3000, 3000 );   	
  	theobject.position.y = AB.randomIntAtoB ( -3000, 3000 ); 
	
 	var r = AB.randomIntAtoB ( 1, 3 );    // random texture from 1-3 for the asteroids
    theobject.material =  new THREE.MeshBasicMaterial ( { map: textureArray[r] } );   

 	ABWorld.scene.add(theobject);
	THEARMY[t] = theobject;	
	t++; 
 }

var shapeShip = new THREE.CylinderGeometry( 150, 75, -200 ); //will be the delcared size
  
var theShip = new THREE.Mesh( shapeShip );
  	
//position of ship
theShip.position.x = 0;
theShip.position.z = 0;
theShip.position.y = 0;


theShip.material =  new THREE.MeshBasicMaterial ( { map: textureArray[19] } );  //TEXTURE 19

ABWorld.scene.add(theShip);
SHIP = theShip;


//Earth
var shapeEarth = new THREE.SphereGeometry( objectsizeE, objectsizeE, objectsizeE ); //will be the delcared size
  
var theEarth  = new THREE.Mesh( shapeEarth );
  	

theEarth.position.x = -1000; 	//position of planet
theEarth.position.z = 0;
theEarth.position.y = 0;
theEarth.radius = 2000;     //radius of planet -> for orbit
theEarth.start = Date.now() //needed for orbit i.e. postion right now


theEarth.material =  new THREE.MeshBasicMaterial ( { map: textureArray[0] } );

ABWorld.scene.add(theEarth);
EARTH = theEarth;


//MARS
var shapeMars = new THREE.SphereGeometry ( objectsizeM, objectsizeM, objectsizeM ); 

var theMars  = new THREE.Mesh( shapeMars );

theMars.position.x = 0;
theMars.position.z = 0;
theMars.position.y = 0;	
theMars.radius = 3000;  //different radius to earth to represent a more accurate orbit
theMars.start = Date.now()
	
theMars.material =  new THREE.MeshBasicMaterial ( { map: textureArray[4] } );   

ABWorld.scene.add(theMars);
MARS = theMars;


//VENUS
var shapeVenus= new THREE.SphereGeometry ( objectsizeV, objectsizeV, objectsizeV); 

var theVenus = new THREE.Mesh( shapeVenus );

theVenus.position.x = -2000;
theVenus.position.z = 0;
theVenus.position.y = 0;
theVenus.radius = 1500;
theVenus.start = Date.now(); //needed for orbit
	
theVenus.material =  new THREE.MeshBasicMaterial ( { map: textureArray[5] } );   

ABWorld.scene.add(theVenus);
VENUS = theVenus;	            


//MERCURY
var shapeMercury = new THREE.SphereGeometry ( objectsizeME, objectsizeME, objectsizeME ); 

var theMercury = new THREE.Mesh( shapeMercury );

theMercury.position.x = -2750;
theMercury.position.z = 0;
theMercury.position.y = 0;
theMercury.radius = 1000;
theMercury.start = Date.now(); //needed for orbit 
	
theMercury.material =  new THREE.MeshBasicMaterial ( { map: textureArray[6] } );   

ABWorld.scene.add(theMercury);
MERCURY = theMercury;


//JUPITER
var shapeJupiter = new THREE.SphereGeometry ( objectsizeJ, objectsizeJ, objectsizeJ ); 

var theJupiter = new THREE.Mesh( shapeJupiter );

theJupiter.position.x = 1500;
theJupiter.position.z = 0;
theJupiter.position.y = 0;
theJupiter.radius = 3750;
theJupiter.start = Date.now() //needed for orbit 


theJupiter.material =  new THREE.MeshBasicMaterial ( { map: textureArray[7] } );   

ABWorld.scene.add(theJupiter);
JUPITER = theJupiter;	            


//SATURN
var shapeSaturn = new THREE.SphereGeometry ( objectsizeS, objectsizeS, objectsizeS);

var theSaturn = new THREE.Mesh( shapeSaturn );

theSaturn.position.x = 3500;
theSaturn.position.z = 0;
theSaturn.position.y = 0;	
theSaturn.radius = 5000;
theSaturn.start = Date.now()
	

theSaturn.material =  new THREE.MeshBasicMaterial ( { map: textureArray[8] } );   

ABWorld.scene.add(theSaturn);
SATURN = theSaturn 


//SRING
var shapeSaturnRing = new THREE.TorusGeometry (800, 100, 100, 100); //Shrunken torus used for the ring for Saturn

var theSaturnRing = new THREE.Mesh( shapeSaturnRing );

theSaturnRing.rotation.x = 200;     //rotated to represent a more accurate version
theSaturnRing.rotation.y = 100;
theSaturnRing.rotation.z = 100;

theSaturnRing.position.x = 3500;
theSaturnRing.position.z = 0;
theSaturnRing.position.y = 0;
theSaturnRing.radius = 5000;
theSaturnRing.start = Date.now() //needed for orbit 

theSaturnRing.material =  new THREE.MeshBasicMaterial ( { map: textureArray[11] } );
    
ABWorld.scene.add(theSaturnRing);
SATURNRING = theSaturnRing         


//URANUS
var shapeUranus = new THREE.SphereGeometry ( objectsizeU, objectsizeU, objectsizeU);

var theUranus = new THREE.Mesh( shapeUranus );

theUranus.position.x = 5000;
theUranus.position.z = 0;
theUranus.position.y = 0;
theUranus.radius = 5750;
theUranus.start = Date.now() //needed for orbit


theUranus.material =  new THREE.MeshBasicMaterial ( { map: textureArray[9] } );   

ABWorld.scene.add(theUranus);
URANUS = theUranus


//URING  
var shapeUranusRing = new THREE.TorusGeometry (500, 20, 20, 20); //same as ring for Saturn, just thinner.
  
var theUranusRing = new THREE.Mesh( shapeUranusRing );

theUranusRing.rotation.x = 0;
theUranusRing.rotation.y = 350; //Rotated to represent a more accurate version 
theUranusRing.rotation.z = 0;

theUranusRing.position.x = 5000;
theUranusRing.position.z = 0;
theUranusRing.position.y = 0;
theUranusRing.radius = 5750;
theUranusRing.start = Date.now() //needed for orbit
	
theUranusRing.material =  new THREE.MeshBasicMaterial ( { map: textureArray[12] } );
    
ABWorld.scene.add(theUranusRing);
URANUSRING = theUranusRing;


//NEPTUNE
var shapeNeptune = new THREE.SphereGeometry ( objectsizeN, objectsizeN, objectsizeN);
  
var theNeptune= new THREE.Mesh( shapeNeptune );

theNeptune.position.x = 6500;
theNeptune.position.z = 0;
theNeptune.position.y = 0;
theNeptune.radius = 6000;
theNeptune.start = Date.now()
	
theNeptune.material =  new THREE.MeshBasicMaterial ( { map: textureArray[10] } );   

ABWorld.scene.add(theNeptune);
NEPTUNE = theNeptune;



var skybox_material_array = [
 	( new THREE.MeshBasicMaterial ( { map: textureArray[13], side: THREE.BackSide } ) ), //needed for our skybox images
 	( new THREE.MeshBasicMaterial ( { map: textureArray[14], side: THREE.BackSide } ) ),
 	( new THREE.MeshBasicMaterial ( { map: textureArray[15], side: THREE.BackSide } ) ),
 	( new THREE.MeshBasicMaterial ( { map: textureArray[16], side: THREE.BackSide } ) ),
 	( new THREE.MeshBasicMaterial ( { map: textureArray[17], side: THREE.BackSide } ) ),
 	( new THREE.MeshBasicMaterial ( { map: textureArray[18], side: THREE.BackSide } ) )
 	];
	
  var skyGeometry = new THREE.CubeGeometry ( skyboxConst, skyboxConst, skyboxConst );	
  var skyMaterial = new THREE.MeshFaceMaterial ( skybox_material_array );
  var theskybox = new THREE.Mesh ( skyGeometry, skyMaterial );

  
  ABWorld.scene.add( theskybox );			
 
  // can start the run loop
  
	ABWorld.render();		
  
	AB.removeLoading();
	
  	AB.runReady = true; 
  	
  	AB.msg ( ` <hr> <p align=\"center\"> <id='para', style=\"background:#CBC3E3;font:italic 0px arial,serif;font-size:large;border: solid #a020f0 \"> Destroy all asteroids before the time runs out!<p>
  	<p align=\"center\"> <b>-----------------------------------------------------------</b><p>
  	<p><b>How to play:</b> (Enter fullscreen for full experience)<p>
  	<p> <id='para', style=\"font: 16px arial,serif \"> 1 - Click and hold to drag the camera to get a better perspective<p>
  	<p> <id='para', style=\"font: 16px arial,serif \"> 2 - Press Start to begin the timer<p>
  	<p> <id='para', style=\"font: 16px arial,serif \"> 3 - Use the arrow keys ↓ ↑️ to move the spaceship up and down, ←  → arrow keys + q & e to move left and right<p>
  	                   <p> <id='para', style=\"font: 16px arial,serif \"> 4 - Get in the proximity of an asteroid with the spaceship, then press spacebar to blow up asteroids <p>
  	                   <p> <id='para', style=\"font: 16px arial,serif \"> 5 - Play by yourself or play with a friend by joining the same world!
  	                   <p align=\"center\"> <b>-----------------------------------------------------------</b><p>
  	                   <p align=\"center\"> <id ="timerP"> <b>You have:</b> <span id="timer"> <b>0</b> </span> <b>seconds remaining!</b> <p>
  	                   <p align=\"center\">  <button onclick='start(); 'id='playAgainButton', style=\"height:50px;width:120px;background-color:#00FF00;font-size:x-large;font:georgia \"> <b>START</b> </button> </p>
  	                   <p> <span id="result"></span> </p>
  	        `);
						
}


function moveArmy()		    // move all the asteroids around the map randomly 
{
 for ( var i = 0; i < THEARMY.length; i++ )
 { 
   if ( THEARMY[i] )		// this is in case initArmy() not called yet 
   { 
        THEARMY[i].position.x =  THEARMY[i].position.x + AB.randomIntAtoB(-WALKSTEP,WALKSTEP) ;        
        THEARMY[i].position.z =  THEARMY[i].position.z + AB.randomIntAtoB(-WALKSTEP,WALKSTEP) ;
        THEARMY[i].position.y =  THEARMY[i].position.y + AB.randomIntAtoB(-WALKSTEP,WALKSTEP) ;
        ABWorld.scene.add( THEARMY[i] );
   }

 }
}


function moveEarth() //here we have our function for our earth to orbit
{
var earthangle = Math.PI*2; //our start angle
var circumference	= EARTH.radius * 2 * Math.PI; //circumfrence
var duration	= 5000; //5 seconds per rotation
var rotSpeed	= 1.25 * Math.PI / duration; //the speed of our rotation (in radian/ms)

        if ( EARTH )
        {
			var delta = Date.now() - EARTH.start;
		    var vector = circumference / duration;
                    // vector * data is a portion of circumference that the dot should have walked through by the duration delta.
                    // You have to normalize by your radius to get an angel (in radian).
			var angle = rotSpeed * delta;  // The angle is now already in radian, no longer need to convert from degree to radian.

            EARTH.position.x =  EARTH.radius * Math.cos(angle) ;        
            EARTH.position.z =  EARTH.radius * Math.sin(angle) ;
            EARTH.position.y =  EARTH.radius * Math.cos(angle) ;
            ABWorld.scene.add( EARTH );
        }
}

function moveMars() //similar to above except for line 421
{
var marsangle = Math.PI*2;
var circumference	= MARS.radius * 2 * Math.PI;
var duration	= 5000; //5 seconds per rotation
var rotSpeed	= 1.25 * Math.PI / duration;

        if ( MARS )
        {
			var delta = Date.now() - MARS.start;
		    var vector = circumference / duration;
                   
			var angle = rotSpeed * delta;

            MARS.position.x =  MARS.radius * Math.cos(angle) ;        
            MARS.position.z =  MARS.radius * Math.sin(angle) ;
            MARS.position.y =  MARS.radius * Math.sin(angle) ; //angle changed go sin from cos for a different rotation.
            ABWorld.scene.add( MARS );
        }
}

function moveVenus() //same as above
{
var venusangle = Math.PI*2;
var circumference	= VENUS.radius * 2 * Math.PI; //circumfrence
var duration	= 5000; //5 seconds per rotation
var rotSpeed	= 1.25 * Math.PI / duration;

        if ( VENUS )
        {
			var delta = Date.now() - VENUS.start;
		    var vector = circumference / duration;
                    
			var angle = rotSpeed * delta;

            VENUS.position.x =  VENUS.radius * Math.cos(angle) ;        
            VENUS.position.z =  VENUS.radius * Math.sin(angle) ;
            VENUS.position.y =  VENUS.radius * Math.sin(angle) ;
            ABWorld.scene.add( VENUS );
        }
}

function moveMercury() 
{
var mercuryangle = Math.PI*2;
var circumference	= MERCURY.radius * 2 * Math.PI; //circumfrence
var duration	= 5050; //5 seconds per rotation
var rotSpeed	= 1.25 * Math.PI / duration;

        if ( MERCURY )
        {
			var delta = Date.now() - MERCURY.start;
		    var vector = circumference / duration;
                   
			var angle = rotSpeed * delta;

            MERCURY.position.x =  MERCURY.radius * Math.cos(angle) ;        
            MERCURY.position.z =  MERCURY.radius * Math.cos(angle) ; //angle changed for different rotation 
            MERCURY.position.y =  MERCURY.radius * Math.sin(angle) ;
            ABWorld.scene.add( MERCURY );
        }
}

function moveJupiter()
{
var jupiterangle = Math.PI*2;
var circumference	= JUPITER.radius * 2 * Math.PI; //circumfrence
var duration	= 5050; //5 seconds per rotation
var rotSpeed	= 1.25 * Math.PI / duration;

        if ( JUPITER )
        {
			var delta = Date.now() - JUPITER.start;
		    var vector = circumference / duration;
		    
			var angle = rotSpeed * delta;

            JUPITER.position.x =  JUPITER.radius * Math.cos(angle) ;        
            JUPITER.position.z =  JUPITER.radius * Math.sin(angle) ;
            JUPITER.position.y =  JUPITER.radius * Math.sin(angle) ;
            ABWorld.scene.add( JUPITER );
        }
}

function moveSaturn()
{
var saturnangle = Math.PI*2, saturnringangle = Math.PI*2
var circumference	= SATURN.radius * 2 * Math.PI, ringcircumference = SATURNRING.radius * 2 * Math.PI;//curcumfrence
var duration	= 5050; //5.05 seconds per rotation
var rotSpeed	= 1.25 * Math.PI / duration;

        if ( SATURN, SATURNRING ) //saturn and its ring called here to ensure they both otbit the same (speed, postion)
        {
			var delta = Date.now() - SATURN.start;
			var deltaring = Date.now() - SATURNRING.start;
		    var vector = circumference / duration;
                    // vector * data is a portion of circumference that the dot should have walked through by the duration delta.
                    // You have to normalize by your radius to get an angel (in radian).
			var angle = rotSpeed * delta;
			var anglering = rotSpeed * deltaring;
			
            SATURN.position.x =  SATURN.radius * Math.cos(angle) ;        
            SATURN.position.z =  SATURN.radius * Math.sin(angle) ;
            SATURN.position.y =  SATURN.radius * Math.sin(angle) ;
            SATURNRING.position.x =  SATURNRING.radius * Math.cos(angle) ;        
            SATURNRING.position.z =  SATURNRING.radius * Math.sin(angle) ;
            SATURNRING.position.y =  SATURNRING.radius * Math.sin(angle) ;
            
            ABWorld.scene.add( SATURN, SATURNRING);
        }
}

function moveUranus()
{
var uranusnangle = Math.PI*2, uranusringangle = Math.PI*2
var circumference	= URANUS.radius * 2 * Math.PI, ringcircumference = URANUSRING.radius * 2 * Math.PI;//circumfrence
var duration	= 5050; //5050 seconds per rotation
var rotSpeed	= 1.25 * Math.PI / duration;

        if ( URANUS, URANUSRING ) //uranus and its ring called here to ensure they both otbit the same (speed, postion)
        {
			var delta = Date.now() - URANUS.start;
			var deltaring = Date.now() - URANUSRING.start;
		    var vector = circumference / duration;
                    // vector * data is a portion of circumference that the dot should have walked through by the duration delta.
                    // You have to normalize by your radius to get an angel (in radian).
			var angle = rotSpeed * delta;
			var anglering = rotSpeed * deltaring;
			
            URANUS.position.x =  URANUS.radius * Math.cos(angle) ;        
            URANUS.position.z =  URANUS.radius * Math.sin(angle) ;
            URANUS.position.y =  URANUS.radius * Math.sin(angle) ;
            URANUSRING.position.x =  URANUSRING.radius * Math.cos(angle) ;        
            URANUSRING.position.z =  URANUSRING.radius * Math.sin(angle) ;
            URANUSRING.position.y =  URANUSRING.radius * Math.sin(angle) ;
            
            ABWorld.scene.add( URANUS, URANUSRING);
        }
}
function moveNeptune()
{
var neptuneangle = Math.PI*2;
var circumference	= NEPTUNE.radius * 2 * Math.PI; //circumfrence
var duration	= 4000; //4 seconds per rotation, faster speed to make a more natural looking orbit
var rotSpeed	= 1.25 * Math.PI / duration;

        if ( NEPTUNE )
        {
			var delta = Date.now() - NEPTUNE.start;
		    var vector = circumference / duration;
                    // vector * data is a portion of circumference that the dot should have walked through by the duration delta.
                    // You have to normalize by your radius to get an angel (in radian).
			var angle = rotSpeed * delta;

            NEPTUNE.position.x =  NEPTUNE.radius * Math.cos(angle) ;        
            NEPTUNE.position.z =  NEPTUNE.radius * Math.sin(angle) ;
            NEPTUNE.position.y =  NEPTUNE.radius * Math.sin(angle) ;
            ABWorld.scene.add( NEPTUNE );
        }
}


document.addEventListener("keydown", function(event) //used to check key numbers
{
  console.log(event.which);
})


var ACTION_LEFT = 200, ACTION_RIGHT = 2367, ACTION_UP = 768, ACTION_DOWN = 9822, ACTION_IN = 1111, ACTION_OUT = 4096584,  EXPLODE = 41900
//all given random numbers


AB.world.newRun = function() 
{
    initMusic(); //for our music to work
    
	AB.loadingScreen();

	AB.runReady = false;  

	ABWorld.init3d ( startRadiusConst, maxRadiusConst, SKYCOLOR  );

	load_resources();
	

	
	document.onkeydown 	= keyHandler;
 
};

AB.world.nextStep = function()
{
 	moveArmy();
    moveEarth();
    moveMars();
    moveVenus();
    moveMercury();
    moveJupiter();
    moveSaturn();
    moveUranus();
    moveNeptune();


};


// What to do when the timer runs out
function gameOver() {
  // This cancels the setInterval, so the updateTimer stops getting called
  try {cancelInterval(timer);} catch (e){ console.log(e);}
  var result = "";
  if ( score == ARMYSIZE )
  result = "<p align=\"center\"> <b>Thanks for playing our game!</b> <br><br> <b>Refresh the page to play again!</b></p>";
  else
    result = "<p align=\"center\"> <b>Thanks for playing our game!</b> <br><br> <b>Refresh the page to play again!</b></p>";
    
  $("#result").html(result);
  
  $("#timerP").hide();
  
   $("#result").show();
  
  // re-show the button, so they can start it again
}

function updateTimer() {
  timeLeft = timeLeft - 1;
  if (timeLeft === 0)  gameOver();
  else if (timeLeft > 0)
  {
  $("#timer").html(timeLeft);
  }
}

//function resetA()
//{
   //for ( var c = 0 ; c < THEARMY.length ; c++ )
   //THEARMY[c].material =  new THREE.MeshBasicMaterial ( { map: textureArray[ AB.randomIntAtoB ( 1, 3 )] } );

//}

// The button has an on-click event handler that calls this
function start() {
  // setInterval is a built-in function that will call the given function
  // every N milliseconds (1 second = 1000 ms)
  timer = setInterval(updateTimer, 1000);
  timeLeft = 300;
  $("#timerP").show();
  // It will be a whole second before the time changes, so we'll call the update
  // once ourselves
  $("#result").hide();
  updateTimer();

  // We don't want the to be able to restart the timer while it is running,
  // so hide the button.
  $("#playAgainButton").hide();
  //resetA();
}


//--- Socket functionality -----------------------------------------------------

// start socket


function moveLogicalAgent( a )			// this is called by the key/touch handlers, not by the infrastructure   
{ 
      if ( a == ACTION_LEFT )
      SHIP.position.x = SHIP.position.x - 100; //move ship -50 on the x axis -> move left
 else if ( a == ACTION_RIGHT )
    SHIP.position.x = SHIP.position.x + 100; //move ship +50 on the x axis -> move right
 else if ( a == ACTION_UP )
 SHIP.position.y = SHIP.position.y - 100; //move ship -50 on the y axis -> move down
 else if ( a == ACTION_DOWN )
 SHIP.position.y = SHIP.position.y + 100; //move ship +50 on the y axis -> move up
 else if (a == ACTION_IN )
 SHIP.position.z = SHIP.position.z - 100; //move ship -50 on the z axis -> move inwards
  else if (a == ACTION_OUT )
 SHIP.position.z = SHIP.position.z + 100; //move ship +50 on the z axis -> move outwards
}

function explodeAsteroids(closestasteroid2ship) //this function explodes asteroids which are closest to the ship
{
score = score + 1;

var min_distance = 999999; //a large number for our min_distance 
if (! closestasteroid2ship)

 for ( var c = 0 ; c < THEARMY.length ; c++ ) //our loop here will determine which asteroid is closest.

 {
  
     var distanceship2as = SHIP.position.distanceTo(THEARMY[c].position); //distance fron our ship to asteroid is equal to the distance of the position of our ship to the distance of the position of the closest asteroid.
     if (distanceship2as < min_distance)
     {
         min_distance = distanceship2as; //the min_distance is now equal to the distance above
         closestasteroid2ship = c;
     }
     
     
 }
  console.log("llllllllllllll"); //some testing done for distance
 THEARMY[closestasteroid2ship].material =  new THREE.MeshBasicMaterial ( { map: textureArray[20] } );      
 
 return closestasteroid2ship;

}

AB.socketStart();

var OURKEYS = [ 37, 38, 39, 40, 81, 69, 32]; //our key codes for movement and explode

function ourKeys ( event ) { return ( OURKEYS.includes ( event.keyCode ) ); }
	
function keyHandler ( event )		
{
	if ( ! AB.runReady ) return true; 		// not ready yet 

    // if not handling this key, send it to default: 
	
	if ( ! ourKeys ( event ) ) return true;
	
	// else handle it and prevent default:
	
	if ( event.keyCode == 37 )   { moveLogicalAgent( ACTION_LEFT 	); moveSounds(); musicPause(); } //if we press left on keyboard we move right and pause the music to start the game
    if ( event.keyCode == 38 )   { moveLogicalAgent( ACTION_DOWN  	); moveSounds(); musicPause(); } //if we press down on keyboard we move right and pause the music to start the game
    if ( event.keyCode == 39 )   { moveLogicalAgent( ACTION_RIGHT 	); moveSounds(); musicPause(); } //if we press right on keyboard we move right and pause the music to start the game
    if ( event.keyCode == 40 )   { moveLogicalAgent( ACTION_UP		); moveSounds(); musicPause(); } //if we press up on keyboard we move right and pause the music to start the game
    if ( event.keyCode == 81 )   { moveLogicalAgent( ACTION_IN      ); moveSounds(); musicPause(); } //if we press q on keyboard we move right and pause the music to start the game
    if ( event.keyCode == 69 )   { moveLogicalAgent( ACTION_OUT		); moveSounds(); musicPause(); } //if we press e on keyboard we move right and pause the music to start the game
    if ( event.keyCode == 32 )   { fireMissile(); AB.socketOut(explodeAsteroids());} //if we press spacebar on keyboard we blow up the asteroid with sound effect and it appears on other players screen
	
	event.stopPropagation(); event.preventDefault(); return false;
}

AB.socketIn = function(closestasteroid2ship)       // incoming data on socket, i.e. clicks of other player 
{
    if ( ! AB.runReady ) return;
    explodeAsteroids(closestasteroid2ship)
};

function fireMissile()
{
 	var x = "<audio    src=/uploads/dg/boom.wav  autoplay  > </audio>"; //https://mixkit.co/free-sound-effects/explosion/
 	$("#user_span2").html( x );
}

function moveSounds()
{
 	var x = "<audio    src=/uploads/dg/move.mp3   autoplay  > </audio>"; //https://pixabay.com/sound-effects/search/whoosh/?manual_search=1&order=None @Natty23
 	$("#user_span3").html( x );
}


function initMusic()
{
	// put music element in one of the spans
  	var x = "<audio  id=theaudio  src=/uploads/dg/spacetheme.mp3  autoplay loop> </audio>" ;
  	$("#user_span5").html( x );
} 
 

function musicPlay()  
{
	// jQuery does not seem to parse pause() etc. so find the element the old way:
 	document.getElementById('theaudio').play();
}

function musicPause() 
{   //function to pause our music once the game starts -> once you move
 	document.getElementById('theaudio').pause();
}
