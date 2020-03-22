---
layout:post
title:Adruion常用函数
date:2020-03-22  
cover:![85KhvQ.jpg](https://s1.ax1x.com/2020/03/22/85KhvQ.jpg)
categories:Adruion
tags:Adruion
---
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title>Adruion常用函数</title>
	</head>
	<body>
		<h1>Adruion常用函数</h1>
		<p>pinMode(pin, mode)<br>
将数位脚位(digital pin)指定为输入或输出。<br>
范例 :pinMode(7,INPUT); // 将脚位 7 设定为输入模式<br>
<br>
digitalWrite(pin, value)<br>
将数位脚位指定为开或关。脚位必须先透过pinMode明示为输入或输出模式digitalWrite才能生效。<br>
范例 :digitalWrite(8,HIGH); //将脚位 8设定输出高电位<br>
<br>
int digitalRead(pin)<br>
将输入脚位的值读出，当感测到脚位处于高电位时时回传HIGH，否则回传LOW。<br>
范例 :val = digitalRead(7); // 读出脚位 7 的值并指定给 val<br>
<br>
int analogRead(pin)<br>
读出类比脚位的电压并回传一个 0到1023 的数值表示相对应的0到5的电压值。<br>
范例 :val = analogRead(0); //读出类比脚位 0 的值并指定给 val变数<br>
<br>
analogWrite(pin, value)<br>
改变PWM脚位的输出电压值，脚位通常会在3、5、6、9、10与11。Value变数范围0-255，例如：输出电压2.5伏特（V），该值大约是128。<br>
范例 :analogWrite(9,128); // 输出电压约2.5伏特（V）<br>
<br>
unsigned long pulseIn(pin, value)<br>
设定读取脚位状态的持续时间，例如使用红外线、加速度感测器测得某一项数值时，在时间单位内不会改变状态。<br>
范例 :time = pulsein(7,HIGH); // 设定脚位7的状态在时间单位内保持为HIGH<br>
<br>
shiftOut(dataPin, clockPin, bitOrder, value)<br>
把资料传给用来延伸数位输出的暂存器，函式使用一个脚位表示资料、一个脚位表示时脉。bitOrder用来表示位元间移动的方式（LSBFIRST最低有效位元或是MSBFIRST最高有效位元），最后value会以byte形式输出。此函式通常使用在延伸数位的输出。<br>
范例 :shiftOut(dataPin, clockPin, LSBFIRST, 255);<br>
<br>
unsigned long millis()<br>
回传晶片开始执行到目前的毫秒<br>
范例:duration = millis()-lastTime; // 表示自"lastTime"至当下的时间<br>
<br>
delay(ms)<br>
暂停晶片执行多少毫秒<br>
范例:delay(500); //暂停半秒（500毫秒）<br>
<br>
delay Microseconds(us)<br>
暂停晶片执行多少微秒<br>
范例:delayMicroseconds(1000); //暂停1豪秒<br>
<br>
min(x, y)<br>
回传两数之间较小者<br>
范例：val = min(10,20); // 回传10<br>
<br>
max(x, y)<br>
回传两数之间较大者<br>
范例：val = max(10,20); // 回传20<br>
<br>
abs(x)<br>
回传该数的绝对值，可以将负数转正数。<br>
范例：val = abs(-5); // 回传5<br>
<br>
constrain(x, a, b)<br>
判断x变数位于a与b之间的状态。x若小于a回传a；介于a与b之间回传x本身；大于b回传b<br>
范例：val = constrain(analogRead(0), 0, 255); // 忽略大于255的数<br>
<br>
map(value, fromLow, fromHigh, toLow, toHigh)<br>
将value变数依照fromLow与fromHigh范围，对等转换至toLow与toHigh范围。时常使用于读取类比讯号，转换至程式所需要的范围值。<br>
例如：val = map(analogRead(0),0,1023,100, 200); // 将analog0 所读取到的讯号对等转换至100 – 200之间的数值。<br>
<br>
double pow(base, exponent)<br>
回传一个数(base)的指数(exponent)值。<br>
范例：double x = pow(y, 32); // 设定x为y的32次方<br>
<br>
double sqrt(x)<br>
回传double型态的取平方根值。<br>
范例：double a = sqrt(1138); // 回传1138平方根的近似值 33.73425674438<br>
<br>
double sin(rad)<br>
回传角度（radians）的三角函数sine值。<br>
范例：double sine = sin(2); // 近似值 0.90929737091<br>
<br>
double cos(rad)<br>
回传角度（radians）的三角函数cosine值。<br>
范例：double cosine = cos(2); //近似值-0.41614685058<br>
<br>
double tan(rad)<br>
回传角度（radians）的三角函数tangent值。<br>
范例：double tangent = tan(2); //近似值-2.18503975868<br>
<br>
randomSeed(seed)<br>
产生乱数，事实上在Arduino里的乱数是可以被预知的。所以如果需要一个真正的乱数，可以呼叫此函式重新设定产生乱数种子。你可以使用乱数当作乱数的种子，以确保数字以随机的方式出现，通常会使用类比输入当作乱数种子，藉此可以产生与环境有关的乱数（例如：无线电波、宇宙雷射线、电话和萤光灯发出的电磁波等）。<br>
范例：randomSeed(analogRead(5)); // 使用类比输入当作乱数种子<br>
<br>
long random(max)<br>
long random(min, max)<br>
回传指定区间的乱数，型态为long。如果没有指定最小值，预设为0。<br>
范例：  long randnum = random(0, 100); // 回传0 – 99 之间的数字<br>
long randnum = random(11); // 回传 0 -10之间的数字<br>
<br>
Serial.begin(speed)<br>
你可以指定Arduino从电脑交换讯息的速率，通常我们使用9600 bps。当然也可以使用其他的速度，但是通常不会超过115,200 bps（每秒位元组）。<br>
范例：Serial.begin(9600);<br>
<br>
Serial.print(data)<br>
Serial.print(data, encoding)<br>
经窗口埠传送资料，提供编码方式的选项。如果没有指定，预设以一般文字传送。<br>
范例：<br>
Serial.print(75); // 列印出 "75"<br>
Serial.print(75, DEC); //列印出 "75"<br>
Serial.print(75, HEX); // "4B" (75 的十六进位)<br>
Serial.print(75, OCT); // "113" (75 in的八进位)<br>
Serial.print(75, BIN); // "1001011" (75的二进位)<br>
Serial.print(75, BYTE); // "K" (以byte进行传送，显示以ASCII编码方式)<br>
<br>
Serial.println(data)<br>
Serial.println(data, encoding)<br>
与Serial.print()相同，但会在资料尾端加上换行字元（ ）。意思如同你在键盘上打了一些资料后按下Enter。<br>
范例：<br>
Serial.println(75); //列印出"75 "<br>
Serial.println(75, DEC); //列印出"75 "<br>
Serial.println(75, HEX); // "4B "<br>
<br>
int Serial.available()<br>
回传有多少位元组（bytes）的资料尚未被read()函式读取，如果回传值是0代表所有窗口资料都已经被read()函式读取。<br>
范例：int count = Serial.available();<br>
<br>
int Serial.read()<br>
读取1byte的窗口资料<br>
范例：int data = Serial.read();<br>
<br>
Serial.flush()<br>
有时候因为资料速度太快，超过程式处理资料的速度，你可以使用此函式清除缓冲区内的资料。经过此函式可以确保缓冲区(buffer)内的资料都是最新的。<br>
范例：Serial.flush();<br>
</p>
	</body>
</html>
