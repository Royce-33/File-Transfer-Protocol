# File-Transfer-Protocol
Reliable file transfer protocol implmented on top of Java's **DatagramSocket** API.

## Protocol
Both sender and receiver applications utilize **Stop and Wait** protocol.

## Sender Application
Located in the Sender file structure, the Sender application has a basic GUI made in **Swing**.

![ScreenShot](Resources/sender_gui.png)

### Arguments
* Receiving application's IPv4 address
* UDP port number to be used for acknowledgements
* UDP port number to be used for sending data
* Name of file to be sent to receiving application (.txt file)
* Timeout (in μs) - how long the Sender will wait for an acknowledgement for a packet before resending it
* Reliable/Unreliable Sending radio buttons:
  * If "Reliable Sending" or none of the buttons is clicked, the Sender will send reliably (i.e no packet loss)
  * If "Unreliable Sending" is clicked, the Sender will simulate packet loss by "dropping" every 10th packet

### Other GUI Components
* Current number of sent in-order packets counter:
  * Counter that updates whenever a packet is successfully sent to the receiving application
* Textbox in the bottom left:
  * Status box that displays the results of the Sender's actions when either "ISALIVE?" or "SEND" is pressed

### Buttons

#### "ISALIVE?" Button
When pressed, sends a packet to check the status of the receiving application, and displays the results in the status box in the bottom left of the GUI.

#### "SEND" Button
When pressed, reads through the given file, creates packets of size 8 bytes, and sends those packets in-order following **Stop and Wait** protocol. If running in unreliable mode, every 10th packet is "dropped" and the Sender times out and resends the current packet.

## Receiver Application
Located in the Receiver file structure, it is a command-line application that receives packets from the Sender application. Everytime a packet is received and the appropriate acknowledgement back to the Sender application.

Command to run it in command-line looks like the following:

"java Receiver Sender_IP UDP_Port_Number UDP_Port_Number filename"  

The first UDP port is the port the receiver uses to receive data, the second is the port used by the sender to recieve acknowledgements. The filename is the name of the file the received data will be stored in, usually .txt files.

**Note**: The given file name does not have to exist when you run the receiver, if it does not exist, the application will create it in it's folder.


For example:

