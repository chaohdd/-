/*!
 * MindPlus
 * mpython
 *
 */
#include <MPython.h>
#include <DFRobot_Iot.h>
// 函数声明
void obloqMqttEventT1(String& message);
// 静态常量
const String topics[5] = {"B-G-5IFGg","aZ785SKMR","","",""};
const MsgHandleCb msgHandles[5] = {NULL,obloqMqttEventT1,NULL,NULL,NULL};
// 创建对象
DFRobot_Iot myIot;


// 主程序开始
void setup() {
	mPython.begin();
	myIot.setMqttCallback(msgHandles);
	myIot.wifiConnect("hhh", "5832615ASD");
	while (!myIot.wifiStatus()) {yield();}
	display.setCursorLine(1);
	display.printLine("热点连接成功");
	myIot.init("iot.dfrobot.com.cn","c9r0IiKMR","","5r9AIiKMRz",topics,1883);
	myIot.connect();
	while (!myIot.connected()) {yield();}
	display.setCursorLine(2);
	display.printLine("MQTT连接成功");
}
void loop() {
	if ((buttonA.isPressed())) {
		myIot.publish(topic_0, "你好呀！");
		display.setCursorLine(3);
		display.printLine("发送成功！");
	}
}


// 事件回调函数
void obloqMqttEventT1(String& message) {
	buzz.play(DADADADUM, Once);
	display.setCursorLine(4);
	display.printLine(message);
}
