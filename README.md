# WhatsApp-using-Node-JS

Read all the received WhatsApp message in Node server and send automatic reply using Node.js

## Installation Steps

1. Clone this repository
2. Install below packages
   Whats App Web: ```  npm i whatsapp-web.js ```
   QR code generator:  ``` $ npm i qrcode-terminal ```

## Screenshots:
<img src='https://user-images.githubusercontent.com/15896579/132215861-5319407d-b446-4d96-866b-4c21e26886d7.png' alt="Project image"/>
<img src='https://user-images.githubusercontent.com/15896579/132215816-aa05b5b1-3ce3-44c6-8a66-e35fd1278bb0.png' alt="Project image"/>
<img src='https://user-images.githubusercontent.com/15896579/132215764-3a80e6b9-9589-477f-b577-4e0db0e7171c.png' alt="Project image"/>


## Video:
https://www.loom.com/share/9f5d3b2a63104029bbfbb76ecc9aa57e

## Source

```
const qrcode = require('qrcode-terminal');

const { Client } = require('whatsapp-web.js');
const client = new Client();

// Get QR code to scan WhatsAPP
client.on('qr', qr => {
    qrcode.generate(qr, {small: true});
});

client.on('ready', () => {
    console.log('Client is ready!');
});

client.on('message', message => {
	console.log(message.body);
});

// Data for WhatsApp
var data = [
    { id: 1, received: 'Hello', reply: 'Hi'},
    { id: 2, received: 'Sorry', reply: 'No problem'},
    { id: 3, received: 'Can we have a call?', reply: 'Please leave a voicemail. Let us connect in an hour. Kind Reards, Amir Mustafa'},
    { default: 'Please leave a voicemail. Let us connect in an hour. Kind Reards, Amir Mustafa' }
];

client.on('message', message => {
    var selectedData = data.find((msg) => {
        if(msg.received === message.body) {
            return true
        }
    });
    var sourceMsg, targetMsg;
    
    if(selectedData && Object.keys(selectedData).length !== 0 && selectedData.constructor === Object) {
        sourceMsg = selectedData.received;
        targetMsg = selectedData.reply;
    }

    // test data
    // const sourceMsg = 'Hello';
    // const targetMsg = 'I am occupied at present. You can leave me SMS here, will call you shortly.';

    // send message
	if(message.body === sourceMsg) {
		message.reply(targetMsg);
	} else {
        message.reply(data.default);
    }
});

client.initialize();
```

## Reference:
https://amirmustafaofficial.medium.com/sending-automatic-whatsapp-messages-using-javascript-9860ba96d486
https://guide.wwebjs.dev/


