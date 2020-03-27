# newchallenge3
// Created on Fri March 27 2020
int l_motor = 0;
int r_motor = 2;
int speed = 50; 
int slow = 20;
int target = 200;
int pause = 300;
int right_range = 2;
int left_range = 0;
int middle_range = 1;
int black_target = 800;
int tophat = 5;
	
int main(){	
	
wallrun();
turn_right();
turn_left();
msleep(400);
findline();
followline();
}

void forwards(){
   motor(l_motor,speed); // go forward 
   motor(r_motor,speed);
}

void turn_right(){
   motor(l_motor,speed); // turn right
   motor(r_motor,-speed);
}

void turnLeft(){ // turn left  
 motor(l_motor,-speed);
 motor(r_motor,speed);
 msleep(600);
 forwards();
 msleep(1500);
 ao();   
}

void turn_left() {
    motor(l_motor,-speed);
    motor(r_motor,speed);
}

void veer_left(){
	motor(r_motor,speed);
	motor(l_motor,slow);
}

void veer_right() {
	motor(r_motor,slow);
	motor(l_motor,speed);
}

void findline(){

while(analog (tophat) < target){ // until the tophat sensor sees the black line go foward
     forwards();
     }
     ao(); 
     printf("found line!\n"); 
     }

void followline() {
	
while (analog(middle_range) > target){ // follow the line until it finds the wall
       printf("starting line follow!\n");
	   
   if (analog(tophat) > black_target){ // stay close to the line
      veer_left();
      printf("vearing left!\n");
      } 
  
   if (analog(tophat) < black_target){ // stay close to the line
     veer_right();
     printf("vearing right!\n");
     }
     ao();
	
}

void wallrun(){ 
     while(analog(left_range) >= target) { 
    
 if (analog(right_range) >= target){ 
        veer_left(); //veering left 
        printf("veer away!/n"); // makes the robot print veer away left on the screen
         }

  if (analog(right_range) >= target){
       veer_right(); // veer right
       printf("veer toward wall!/n"); //veer towards the wall
  }
 
}
