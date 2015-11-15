////////Project 3. First Draft/////////String title=  "cst112 project3";
String author=  "Brian Salaway";
float left, right, top, bottom;
float middle= width/2;
//////////////////////////buttons
float button2X= left+125, button2H=top+25, button2W=left+175, button2Y=top+50; ///
float button4X=left+625, button4H=top+25, button4W=left+675, button4Y=top+50;

/////////////////////////////////balls
float cueX, cueY, cueDX, cueDY;
float redX,  redY,  redDX,  redDY;
float yelX,  yelY,  yelDX,  yelDY;
float bluX, bluY, bluDX, bluDY;
float oraX, oraY, oraDX, oraDY; /////////////////////////
float cloudY, cloudX, cloudDX, cloudDY;


boolean wall=true;
int grassX=1;
int grassY=460;
int spacing=3;
int len=40;
int endlegs=700;
//// SETUP:  size and table
void setup() {
  
  size( 700, 500 );
  left=   50;
  right=  width-50;
  top=    100;
  bottom= height-100;
  middle= left + (right-left) / 2;///////////////////////////////////////

  
 
  fill(0,255,0);
while(grassX<=endlegs){
  rect(grassX,grassY,2,grassY+len);
  grassX=grassX+spacing; }   
  
  reset();
}
void reset(){
{
  
  cueX=  left + (right-left) / 4;
   cueY=  top + (bottom-top) / 2;
  ///////////////////random positions of balls
   redX=  random( width/2 ,right );   redY=  random( top, bottom );
   bluX=  random( width/2,right );   bluY=  random( top, bottom );
   yelX=  random( width/2,right );   yelY=  random( top, bottom );
   oraX=  random(width/2,right);     oraY=  random(top, bottom);
   cloudX=10;                        cloudY=10;
  
 {  // Random speeds
   redDX=  random( 1,3 );   redDY=  random( 1,3 );
   bluDX=  random( 1,3 );   bluDY=  random( 1,3 );
   yelDX=  random( 1,3 );   yelDY=  random( 1,3 );
   oraDX=  random(1,3) ;     oraDY=  random(1,3);
   cloudDX = (-1);                cloudDY=(0);
}
int spacing=100;
int len=10;
for( cloudX=10; cloudX<=700; cloudX+=spacing){
  stroke(10);
  fill(250);
  ellipse(cloudX,cloudY, 60,cloudY);

}
}
}
 //// NEXT FRAME:  table, bounce off walls, collisions, show all
void draw() {
  {

 rectMode( CORNERS );
  table( left, top, right, bottom );
  bounce();
  collisions();
show();
messages();

  } 
}



//// SCENE:  draw the table with walls

void table( float left, float top, float right, float bottom ) {
  fill( 0, 200, 50 );    // green pool table
  strokeWeight(20);
  stroke( 127, 0, 0 );      // Brown walls
  rect( left-20, top-20, right+20, bottom+20 );

 ////////////////////////////buttons
     
strokeWeight(0);  
fill(0);  
  rect(button2X, button2Y, button2W, button2H);///////////wall button
  fill(255);
  text("wall", button2X+10, button2Y-10);
  fill(0);
  rect(button4X, button4Y, button4W, button4H);///////////reset button
fill(255);
text("reset", button4X+10, button4Y-10);

  if (wall){
  float middle=(left+right)/2;
  stroke(0,127,0);
  strokeWeight (20);
  line (middle, top+10, middle, bottom-10);} else {middle=left;}

if (wall){
   middle=(left+right)/2;} 
  }
 
 
//// ACTION:  bounce off walls, collisions
void bounce() {
  cueX +=cueDX; if (cueX<left ||cueX>right) cueDX *= -1;
  cueY +=cueDY; if (cueY<top ||cueY>bottom) cueDY *= -1;

  redX += redDX;  if ( redX<middle+10 || redX>right ) redDX *= -1;
  redY += redDY;  if ( redY<top || redY>bottom ) redDY *=  -1;

  yelX += yelDX;  if ( yelX<middle+10 || yelX>right ) yelDX *= -1;
  yelY += yelDY;  if ( yelY<top || yelY>bottom ) yelDY *=  -1;
  
  bluX += bluDX;  if ( bluX<middle+10 || bluX>right ) bluDX *= -1;
  bluY += bluDY;  if ( bluY<top || bluY>bottom ) bluDY *=  -1;  
  
   oraX += oraDX;  if ( oraX<middle+10 || oraX>right ) oraDX *= -1;
  oraY += oraDY;  if ( oraY<top || oraY>bottom ) oraDY *=  -1;  
  
 cloudX += cloudDX; 
}
void collisions() {
  float tmp;
  // Swap velocities!
  if ( dist( redX,redY, yelX,yelY ) < 30 ) {
    tmp=yelDX;  yelDX=redDX;  redDX=tmp;
    tmp=yelDY;  yelDY=redDY;  redDY=tmp;}
    
  if ( dist( bluX,bluY, yelX,yelY ) < 30 ) {
    tmp=yelDX;  yelDX=bluDX;  bluDX=tmp;
    tmp=yelDY;  yelDY=bluDY;  bluDY=tmp;}
     
      if ( dist( redX,redY, bluX,bluY ) < 30 ) {
    tmp=bluDX;  bluDX=redDX;  redDX=tmp;
    tmp=bluDY;  bluDY=redDY;  redDY=tmp;}   
    
   if ( dist( redX,redY, oraX,oraY ) < 30 ) {
    tmp=oraDX;  oraDX=redDX;  redDX=tmp;
    tmp=oraDY;  oraDY=redDY;  redDY=tmp;}
    
    if( dist( yelX,yelY, oraX,oraY ) < 30 ) {
    tmp=oraDX;  oraDX=yelDX;  yelDX=tmp;
    tmp=oraDY;  oraDY=yelDY;  yelDY=tmp;}
    
    if ( dist( bluX,bluY, oraX,oraY ) < 30 ) {
    tmp=oraDX;  oraDX=bluDX;  bluDX=tmp;
    tmp=oraDY;  oraDY=bluDY;  bluDY=tmp;}     
} 




//// SHOW:  balls, messages
void show() { 
  {
  stroke(0);
  strokeWeight(1);  
  
fill( 255,255,255 );    
ellipse( cueX,cueY, 30,30 );
 
 fill( 255,0,0 );    
  ellipse( redX,redY, 30,30 );  
  fill(0);  
   text( "1", redX,redY );
       
  fill( 255,255,0 );  
  ellipse( yelX,yelY, 30,30 );
   fill(0);
   text( "2", yelX,yelY );
   
  fill( 0,0,255 );    
  ellipse( bluX,bluY, 30,30 );
   fill(0);
   text( "3", bluX,bluY ); 
   
   fill( 0255,128,0 );    
  ellipse( oraX,oraY, 30,30 );
   fill(0);
   text( "4", oraX,oraY ); 
  }
}
void messages(){
}

//// HANDLERS:  keys, click
void keyPressed() {
  if (key == 'r') {
    reset();
  }
  if(key=='w') { wall=false;} 
  if (key=='e') { wall=true;}
 
  if (key =='q') {exit ();}
}  
 void mousePressed(){ //////resetting balls to right side
 
if (  mouseX >= button2X && mouseX <=  button2W 
 && mouseY >= button2H && mouseY <= button2Y)   {wall=false;} 
 
 
  if (  mouseX >= button4X && mouseX <=  button4W 
 && mouseY >= button4H && mouseY <= button4Y)    {
    reset(); wall=true;
  } 
 }
