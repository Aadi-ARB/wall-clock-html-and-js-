/****** wall-clock-html-and-js-
This is an html page which tells you time digitally on wall clock******/
/**
 *      A simple clock (or watch).
 */

/*
                    ██████████  ██████████   ███         ███    ████████
                        ██          ██      ██ ██       ██ ██  ██
                        ██          ██      ██  ██     ██  ██  ███████
                        ██          ██      ██   ██   ██   ██  ██
                        ██          ██      ██    ██ ██    ██  ██
                        ██      ██████████  ██     ███     ██   ████████
*/
/**
                ██    ███   ████████   ████████   ███████    ████████   ███████
                ██  ███    ██         ██         ██     ██  ██         ██     ██
                █████      ███████    ███████    ██     ██  ███████    ██     ██
                █████      ██         ██         ████████   ██         ████████
                ██  ███    ██         ██         ██         ██         ██   ██
                ██    ███   ████████   ████████  ██          ████████  ██    ███
                
                (I know it's called a clock :))
*/

scale(width/400, height/400);

var drawClock;
var writeNums;
var Count = 0;

var T = "";

var HandsPos = {
    hour : 0,
    min : 0,
    sec : 0
};

drawClock = function(){         // Lots of Maths involved in this function
    HandsPos.hour = (hour() + minute()/60 + second()/3600) /12 * 360;
    HandsPos.min = (minute() + second()/60) /60 * 360;
    HandsPos.sec = second()/60 * 360;

    fill(10, 30, 50, (sin(Count*0.8)+1)/2*100);
    ellipse(-130*sin(Count)+200, -130*cos(Count)+150, 80, 80);
    ellipse(-130*sin(Count+120)+200, -130*cos(Count+120)+150, 80, 80);
    ellipse(-130*sin(Count+240)+200, -130*cos(Count+240)+150, 80, 80);
    fill(10, 30, 50, (sin(Count*0.8+180)+1)/2*100);
    ellipse(130*sin(Count+60)+200, -130*cos(Count+60)+150, 80, 80);
    ellipse(130*sin(Count+180)+200, -130*cos(Count+180)+150, 80, 80);
    ellipse(130*sin(Count+300)+200, -130*cos(Count+300)+150, 80, 80);

    stroke(30, 127, 255, 180);
    strokeWeight(2);
    fill(20, 50, 80, 180);
    ellipse(200, 150, 200, 200);        // Clock Body
    noStroke();
    ellipse(200, 150, 150, 150);        // Inner Circle
    ellipse(200, 150, 100, 100);        // Innermost Circle

    writeNums();

    stroke(255, 30, 127);
    strokeWeight(6);
    line(200, 150, 55*sin(HandsPos.hour)+200, -55*cos(HandsPos.hour)+150);      // Hour Hand
    strokeWeight(3);
    line(200, 150, 75*sin(HandsPos.min)+200, -75*cos(HandsPos.min)+150);        // Minute Hand
    strokeWeight(1.5);
    line(-20*sin(HandsPos.sec)+200, 20*cos(HandsPos.sec)+150, 90*sin(HandsPos.sec)+200, -90*cos(HandsPos.sec)+150);        // Second Hand

    stroke(30, 127, 255);
    strokeWeight(8);
    point(200, 150);
};

writeNums = function(){
    textSize(15);
    fill(255, 80, 20);
    text("1", 242, 77);         // Numbers on the clock
    text("2", 275, 110);
    text("3", 287, 155);
    text("4", 275, 200);
    text("5", 242, 233);
    text("6", 195, 245);
    text("7", 152, 233);
    text("8", 119, 200);
    text("9", 107, 155);
    text("10", 119, 110);
    text("11", 152, 77);
    text("12", 190, 70);
    
    strokeWeight(5);
    stroke(70, 180, 255);
    point(200, 50);             // Hour Marks
    point(250, 63);
    point(287, 100);
    point(300, 150);
    point(287, 200);
    point(250, 237);
    point(200, 250);
    point(150, 237);
    point(113, 200);
    point(100, 150);
    point(113, 100);
    point(150, 63);
};

draw = function() {
    background(0, 0, 0);

    fill(10, 15, 30);
    noStroke();
    rect(50, 25, 300, 350);

    drawClock();

    textFont("arial", 30);

    if(hour() > 12){
        T = hour() - 12;
    }
    else{
        T = hour();
    }

    if(hour() === 0){
        T = 12;
    }

    if(T <= 9){
        T = "0" + T;
    }

    T += " : ";
    
    T += (minute() >= 10) ? minute() : "0" + minute(); T += " : ";
    T += (second() >= 10) ? second() : "0" + second();
    if(hour() >= 12){
        T += "  PM";
    }
    else{
        T += "  AM";
    }

    stroke(30, 127, 255, 180);
    strokeWeight(2);
    fill(20, 50, 80, 180);
    rect(80, 300, 250, 40);

    fill(255, 30, 127);
    text(T, 100, 330);
    
    //Count++;
};
