# FPGA Bomb Defuse Game Project (Verilog) 💥💣
 
## Overview
This is a custom hardware-based "bomb defuse" game designed to run on an FPGA development board. The game logic is written entirely in Verilog, and it utilizes a VGA interface to display the game graphics on a standard monitor.

## Game Purpose
The purpose of this game is to defuse a fake bomb before it explodes. There are three "stages" to this bomb defusal, and the player has 3 minutes to complete all three.

* **WIN:** If done so correctly within the time limit, the timer graphics and ticking sound will stop, and the three stage indicator lights will all be lit up in green; the player has won.
* **LOSE:** If any mistake is made during the stages, or the timer ends up running out, the bomb will explode and leave the screen completely red (accompanied by a continuous buzzing sound); the player has lost.

---

 **ACADEMIC INTEGRITY NOTE:** This game was submitted to be graded for the ECE241 course at the University of Toronto. To comply with the university's academic integrity policies regarding the sharing of code, the source code is **NOT included** in this repository.

However, the following is included:
* Compiled bitstream file (**.sof file**)
* Hand-drawn graphic assets (Background and sprite sheets in .bmp)
* Audio files (in **.wav** and **.mif**)

This allows users to download and play the game without exposing the code or logic to future students.

---

## Hardware Requirements
To play this game, you will need the following equipment:

* **FPGA Board:** DE1-SoC Cyclone V (5CSEMA5F31C6)
* **VGA Monitor:** Standard 640x480 screen capability with a VGA port (or any suitable adapter)
* **Speaker:** Any model is fine, as long as it can connect to the audio port on the FPGA.

*(note: the .sof file included in this repository will not work for any other Cyclone V chip, as it will have to be recompiled to match the chip.)*

## Software Requirements
You do not need the full Quartus Prime design suite to play this game. You only need the programmer:

* **Quartus Prime Programmer:** Lite version is free and completely sufficient. When downloading, choose version 18.1 for compatibility.
* Download link: https://www.altera.com/products/development-tools/quartus

## How to load the game
Now that you have your equipment and software, follow these steps to load the game onto your FPGA board:

1.  Download **'top.sof'** from this repository.
2.  Connect the hardware.
    * Plug the FPGA board into power.
    * Connect the computer to the board.
    * Connect the VGA monitor to the board.
    * Turn the FPGA board on.
3.  Program the board with Quartus.
    * Open **Quartus Prime ver 18.1** and create a new project.
    * In the **'tools'** select bar at the top of the screen, locate and open the **programmer**.
    * Click **'Hardware Setup'**, choose **'Auto Detect'**, and select the DE1-SoC board (it should be the only option).
    * Double-click the device in the list and select the **'top.sof'** file you downloaded.
    * Check the box under **"Program/Configure"**.
    * Click **"Start"**.

Once the progress bar hits 100%, the game should immediately appear on your VGA monitor!

---

## How to play
The game is controlled using the on board switches and buttons. The game instructions appear on the VGA monitor, but a more detailed set of instructions is provided below.

### To Start
After the game loads onto the VGA display monitor, the timer will immediately start counting down from 3 minutes.
* Click **KEY[0]** to start the first stage.

---

### Stage 1 - Wire Cutting
In stage 1, the player needs to **cut the 2 safe wires out of the 3 in total**.

To cut a wire, click its corresponding KEY on the board.
* The **RED** wire corresponds to **KEY[3]**.
* The **GREEN** wire corresponds to **KEY[2]**.
* The **BLUE** wire corresponds to **KEY[1]**.

(Like what may happen with a real bomb, this stage depends fully on luck!)

**To confirm/enter, PRESS KEY[0].** If the player succeeds in cutting the two correct wires, the first light at the top right of the bomb screen (stage indicator lights) will light up green.

---

### Stage 2 - Switch Selection
In stage 2, the player needs to **turn on the switches that are indicated and covered on the VGA monitor.**

* Since only switches 4-9 are for switch selection, the player can deduce the correct switches by looking at the uncovered switches on the VGA monitor.

**To confirm/enter your switch selection, PRESS KEY[0].** If the player succeeds, the second stage indicator light will also light up green.

---

### Stage 3 - Morse Code Decoding
In stage 3, the player needs to **decode a code from morse code and then input it in binary on switches 0-3**.

* LEDR[8] will start blinking red. The player needs to distinguish between the long and short blinks to translate the numbers.
* Once the 5 blinks have completed, the board will wait for the player to configure the SW[0-3] to correspond to the correct number in binary.

**To confirm each number input, PRESS KEY[0].** If the player succeeds with every number, the next morse code number will begin to blink. If the player fails, it's an instant game over red screen.

After **6 successful binary number inputs**, the player will have entered the correct code. The third stage indicator light will light up green, and the timer will stop (along with the ticking sound).

**Congratulations! You have successfully defused the bomb!**

---

## **Screenshots and Gameplay**


<h2 align="center">💣 Gameplay Demo</h2>

<p align="center">
  <img src="misc\Example_gameplay.gif" alt="Main Gameplay Loop" width="70%">
  <br>
  <em>Figure 1: Example gameplay from volunteer game testers.</em>
</p>



<table align="center">
  <tr>
    <th width="50%">Monitor View</th>
    <th width="50%">Game Over Sequence</th>
  </tr>
  <tr>
    <td align="center"><img src="misc\game_snapshot.bmp" width="100%" alt="Static Snapshot"></td>
    <td align="center"><img src="misc\Countdown_game_over.gif" width="100%" alt="Game Over"></td>
  </tr>
</table>

