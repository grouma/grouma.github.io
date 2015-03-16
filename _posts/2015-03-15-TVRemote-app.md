---
layout: post
title: IoT Remote
comments: true
summary: Connecting a basic TV to the Internet.
---

I don't subscribe to cable and get most of my video content from Netflix, Hulu and YouTube which is consumed through an Apple TV or Chromecast. This means I can mostly control my TV from my phone, which is always by my side. Unfortunately, changing the input, volume or powering on my TV means I have to use the provided remote. This is a massive pain because I'm constantly losing the device. I end up tearing my living room apart to often find it left in the bathroom or some other random location. After the umpteenth time I decided I was going to do something about it. The solution I came up with was a simple iOS application paired with an Internet connected micro-controller.

### Materials

* <a href="https://www.spark.io/">Spark Core</a>
* <a href="https://www.sparkfun.com/products/10732/">IR Led Kit</a>
* Breadboard and various hookup wires
* iOS device
* Basic Television (mine is an Insignia)

### How it works

The signal between a remote control handset and the device it controls consists of pulses of infrared light. The Spark Core, wired up with an IR led, simply mimics these pulses to control the television. Thanks to the wireless capabilities of the Spark Core, commands can easily be sent from any Internet connected device, in my case an iPhone.

### Finding your TV's control codes

Different manufacturers of infrared remote controls use different protocols to transmit the infrared commands. Thankfully, most televisions protocols and codes have been mapped by the <a href="http://www.lirc.org/">Linux Infrared Remote Control</a> project. 

Although, my Insignia television had the protocol and basic functions mapped, it was missing several key commands. A little light reading on the protocol (<a href="http://www.circuitvalley.com/2013/09/nec-protocol-ir-infrared-remote-control.html">NEC</a>) enabled me to write the following script. 

{% highlight python %}

def intToBinaryString(num, size):
  binaryString = "{0:b}".format(num)
  while len(binaryString) < size:
    binaryString = "0" + binaryString
  return binaryString


def complementBinaryString(string):
  complement = ""
  for bit in string:
    if bit == "0":
      complement += "1"
    else:
      complement += "0"
  return complement

def binaryStringToHex(string):
  return hex(int(string,2))

def hexToBinary(hexval):
        thelen = len(hexval)*4
        binval = bin(int(hexval, 16))[2:]
        while ((len(binval)) < thelen):
            binval = '0' + binval
        return binval

def funcToHexString(num):
  """ Returns the corresponding hex code for provided function number"""
  prefix = intToBinaryString(num,8)[::-1]
  suffix = complementBinaryString(prefix)
  return binaryStringToHex(prefix + suffix)

def hexStringToFunc(hexString):
  """ Returns the corresponding function number for provided hex code"""
  binaryString = hexToBinary(hexString)
  funcString = ""
  for num in range(0, 8):
    funcString += binaryString[num]
  return int(funcString[::-1],2)

funcCodes = ["18E7", "F00F", "00FF", "807F", "40BF", "C03F", "A05F", "20DF", "609F", "E01F", "10EF", "906F", "E817", "08F7", "708F", "B04F", "50AF", "30CF", "D02F", "28D7", "D827", "9867", "48B7", "8877", "38C7","C837"]
funcNums = []
for code in funcCodes:
  funcNums.append(hexStringToFunc(code))
funcNums.sort()
print("Function codes already decoded:")
print(funcNums)

codesToTest = []
for num in range(0,30):
  if num not in funcNums:
    codesToTest.append(funcToHexString(num))
print("Function codes to test:")
print(codesToTest)

{% endhighlight %}

Essentially the script determines which hex codes are missing from an NEC mapping. Instructing the Spark Core to execute a given infrared command and watching the TV's response allowed me to complete the mapping.

### Device and App

![remote close up](/public/images/remote-1.JPG)
![remote and tv](/public/images/remote-2.JPG)
![app](/public/images/remote-3.PNG)

### Code

The code is available on GitHub <a href="https://github.com/grouma/TVRemote">here</a>. I'm not an iOS developer so I thought it would be fun to learn Swift as well. Apologies in advanced for any poor practices. Also a special thanks to Gaspard van Koningsveld as I made use of his <a href="https://github.com/qwertzguy/Spark-Core-IRremote">Spark Core IR Library</a>.

### What's Next

Both my bedroom and living room televisions are from the same manufacture and consequently use the same protocol and commands. I have built in the functionality to switch between Spark Cores. It would also be useful to switch between remote protocols and codes. Finally, I plan on using this project as an excuse to get a 3d printer. This will enable me to create an eye pleasing enclosure. 
