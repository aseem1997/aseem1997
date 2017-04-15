
import curses
import time
import RPi.GPIO as GPIO


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

