import curses
import time
import RPi.GPIO as GPIO

from threading import Thread
import time

 


#raspivid -o - -t 0 -hf -vf -w 1080 -h 768 -fps 24 | cvlc -vvv stream:///dev/stdin --sout  '#standard{access=http,mux=ts,dst=:8160}'  :demux=h264


class Hello5Program:  
    def __init__(self):
        self._running = True

    def terminate(self):  
        self._running = False  

    def run(self):
        global cycle
        while self._running:
            time.sleep(5) #Five second delay
            cycle = cycle + 1.0
            raspivid -o - -t 0 -hf -vf -w 1080 -h 768 -fps 24 | cvlc -vvv stream:///dev/stdin --sout  '#standard{access=http,mux=ts,dst=:8160}'  :demux=h264

	    
class Hello2Program:  
    def __init__(self):
        self._running = True

    def terminate(self):  
        self._running = False  

    def run(self):
        global cycle
        while self._running:
            time.sleep(2) #Five second delay
            cycle = cycle + 0.5
	
            import curses



GPIO.setmode(GPIO.BOARD)
GPIO.setup(10, GPIO.OUT)
GPIO.setup(19, GPIO.OUT)
GPIO.setup(21, GPIO.OUT)
GPIO.setup(37, GPIO.OUT)
GPIO.setup(38, GPIO.OUT)

screen=curses.initscr()
curses.noecho()
curses.cbreak()
screen.keypad(True)

try:
        while True:
                char=screen.getch()

                if char== ord( 'q'):
                        print "Loop terminated"
                        break

                elif char==curses.KEY_UP:
                        GPIO.output(21,GPIO.HIGH)
                        GPIO.output(19,GPIO.LOW)
                        GPIO.output(38,GPIO.HIGH)
                        GPIO.output(37,GPIO.LOW)
                        print "forward"
                        time.sleep(1)

                elif char==curses.KEY_DOWN:
                        GPIO.output(21,GPIO.LOW)
                        GPIO.output(19,GPIO.HIGH)
                        GPIO.output(38,GPIO.LOW)
                        GPIO.output(37,GPIO.HIGH)
                        print "backward"
                        time.sleep(1)

                elif char==curses.KEY_RIGHT:
                        GPIO.output(21,GPIO.LOW)
                        GPIO.output(19,GPIO.HIGH)
                        GPIO.output(38,GPIO.HIGH)
                        GPIO.output(37,GPIO.LOW)
                        print "right"
                        time.sleep(1)

		elif char==curses.KEY_LEFT:
                        GPIO.output(21,GPIO.HIGH)
                        GPIO.output(19,GPIO.LOW)
                        GPIO.output(38,GPIO.LOW)
                        GPIO.output(37,GPIO.HIGH)
                        print "left"
                        time.sleep(1)

                elif char== ord('s'):
                        GPIO.output(19,GPIO.LOW)
                        GPIO.output(21,GPIO.LOW)
                        GPIO.output(37,GPIO.LOW)
                        GPIO.output(38,GPIO.LOW)
                        print "stop"

finally:

        curses.nocbreak()
        screen.keypad(0)
        curses.echo()
        curses.endwin()
        GPIO.cleanup()





            
            
#Create Class
FiveSecond = Hello5Program()
#Create Thread
FiveSecondThread = Thread(target=FiveSecond.run) 
#Start Thread 
FiveSecondThread.start()



#Create Class
TwoSecond = Hello2Program()
#Create Thread
TwoSecondThread = Thread(target=TwoSecond.run) 
#Start Thread 
TwoSecondThread.start()



Exit = False #Exit flag
while Exit==False:
 cycle = cycle + 0.1 
 print "Main Program increases cycle+0.1 - ", cycle
 time.sleep(1) #One second delay
 if (cycle > 5): Exit = True #Exit Program

FiveSecond.terminate()
TwoSecond.terminate()
print "Goodbye :)"



			