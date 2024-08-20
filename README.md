# NeoCard
<br>
 This is a prototype of a PCB business card <b>under $5</b> in which one can play a game and play a video. The project's complete,the code has no bitmap in it,meaning you have to add your very own bitmap for the animation.

# The things this can do:
- [x] Play a video at 10fps
- [x] Run a game (more on that below)
- [x] Transmit NFC messages
- [x] Look cool

![image](https://github.com/user-attachments/assets/5b3fc10e-1e82-4d7a-95fd-9b008305f782)
![image](https://github.com/user-attachments/assets/94e2b29f-5a3e-4bdc-9da0-cf3e8fd23d45)
![image](https://github.com/user-attachments/assets/ae6bb44b-6eeb-40cb-9b7b-73098d19d64d)
![image](https://github.com/user-attachments/assets/b5111bf2-4a36-4320-aa13-574c7865694c)

## how the game works:

* its a cube roaming around in void,symbolising neo in the matrix. while he roams,random messages in the interval 8 seconds display a message amoungst 100 messages.
* one of these 100 messages are displayed,this symbolises Morpheus trying to contact neo.
* the matrix has you,and there is nothing you can do,for you're a cube
>i had to come up with a game idea that runs well in a esp-12f and i assume ive assumed what i wanted to do

![image](https://github.com/user-attachments/assets/0f77c556-c21c-48cb-a877-bf346d251d20)
>what it basically does
## how the video part works:
* entered bitmap data cycles constatntly on a fps of 10
> did so because, im afriad that the esp-12f may lag when given the operation to run the video exceeding 10 fps.The video can only be played in monochrome(white and black according to the parts used)
![image](https://github.com/user-attachments/assets/7f594c91-6d9e-495b-9379-7ae118aa5726)
