# WAWEB-phi
![npm](https://img.shields.io/npm/v/waweb-phi)  ![NPM](https://img.shields.io/npm/l/waweb-phi) ![GitHub last commit](https://img.shields.io/github/last-commit/oqhadev/waweb-phi)

WAWEB-phi is library for controlling whatsapp web for nodejs,
inspired from [whatsapp-web.js](https://github.com/pedroslopez/whatsapp-web.js) and WAPI.js


What is the difference? This library uses wapi.js which contains features such as sending pictures, sending to numbers that are not in the contact list
and many more

## Installation
NPM
```bash
npm install waweb-phi 
```
YARN
```bash
yarn add waweb-phi 
```

## Usage

```js
const wa = require('waweb-phi')

const client = new wa({
    puppeteer: { headless: false }

});


client.initialize();
```



## Example
```js
const wa = require('waweb-phi')

const client = new wa({
    puppeteer: { headless: false },//change it to true if u want hidding the chrome/headles mode
    authTimeout: 30000,
    // u can passing wa session here, and example, just uncoment and change to ur session
    // u can see ur session when u get AUTHENTICATED
    // 
    // session: {
    //     WABrowserId: '"qU5V5x/V2iasdasdTdfH5QdHc7yg=="',
    //     WASecretBundle:
    //         '{"key":"TVCj4p60Jasdasd9nklQDp+hSmK+nvCVMHK2fwID9tpShGQVo=","encKey":"do3JhuI3JvkTAuTs4UNUbZHuHasdasdGjXA+UOopphm5un2b8=","macKey":"TVCj4p60J9nklQDp+hSmK+nvCVMHK2fwID9tpShGQVo="}',
    //     WAToken1: '"F+hVGpk5GwmSNhasdasd1bQYlPaffAL//Oc00Oj9C9VZqWlBQ="',
    //     WAToken2:
    //         '"1@RDZOZEmI8Yxi8m8qw3spzoNK/YqfI8JGLxzWSJ5jeVJVp8faNGDB6asdasdasdLXSuxiA1gvyFeSapmChrc6JfA=="'
    // }



});


client.initialize();


client.on('qr', (qr) => {
    console.log('QR RECEIVED', qr);

});

client.on('authenticated', (session) => {
    console.log('AUTHENTICATED', session);

});

client.on('auth_failure', msg => {
    console.error('AUTHENTICATION FAILURE', msg);


})

client.on('ready', () => {
    console.log('READY');




    
        
    
     

        // send message, u can send to anyone, even if number not saved in ur contact
        client.sendMessage("628950609xxxx@c.us", `test`).then((r) => {
            console.log("sendMessage",r)
        })

        // bingung kata2nya pokoknya event ceklis 1 ceklis 2 ceklis 2 biru
        client.on('ack', (data) => {
            console.log('ACK', data);
        });
        // send Attachment,image/rar/video  anythings
        // convert to base64 first 
        let base64file = `data:image/png;base64,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`
        client.sendAttach(base64file,'caption','namafile.png',"628950609xxxx@c.us").then((r) => {
            console.log("sendMessage",r)
        })


        // get Device Info 
        client.deviceInfo().then((r) => {
            console.log("deviceInfo", r)
        })
        // return
        // { wa_version: '2.20.28',
        // mcc: '510',
        // mnc: '010',
        // os_version: '9',
        // device_manufacturer: 'OPPO',
        // device_model: 'RMX1801',
        // os_build_number: 'RMX1801EX_11_C.26' }


        // get Send Seen 
        client.sendSeen('628950609xxxx@c.us').then((r) => {
            console.log("sendSeen", r)
        })
        
        // get battery level
        client.getBatteryLevel().then((r) => {
            console.log("getBatteryLevel", r)
        })
        



        // cek number status
        let number = "628950609xxxx@c.us"
        client.checkNumberStatus(number).then((r) => {
            console.log("NumberStatus", r)
        })

        // also you can access wapi.js directly


    



});


client.on('message', async msg => {
    console.log('MESSAGE RECEIVED', msg);

});

client.on('disconnected', () => {

    console.log('Client was logged out');
})


```




## Update
- 27/03/2020 (v0.1.16) Update 
- 06/03/2020 (v0.1.15) add ack status (send,received,read) 
- 19/02/2020 (v0.1.14) Add SendImageToID + fix SendImage + add sendSeen + add deviceInfo 
- 27/01/2020 (v0.1.12 > v0.1.13) add authTimeout option + change default authTimeout value from 5000ms to 10000ms , for detail check example.js
- 17/01/2020 (v0.1.11) fix selector qr/qrvalue/keep phoneimage update 

## Todo

- [ ] Implement+fix `important` WAPI.js Function 



## Legal
This code is in no way affiliated with, authorized, maintained, sponsored or endorsed by WhatsApp or any of its affiliates or subsidiaries. This is an independent and unofficial software. Use at your own risk. Commercial use of this code/repo is strictly prohibited.

## License
[APACHE v2](https://www.apache.org/licenses/LICENSE-2.0.txt)



made with 💗 