# FLOW DESIGN PATTERNS IN NODE-RED

## Sample data every 1 second

<div align="center">
<img src="https://github.com/hoat23/IndustrialInternetOfThings/blob/master/img/flow_design_patterns/flow_sampling_data_every_1sec.png" width="500" align="center"/>
</div>


```
[{"id":"db2a91a4.568308","type":"inject","z":"f30d21db.d2c33","name":"Run","props":[{"p":"payload","v":"run","vt":"str"},{"p":"topic","v":"","vt":"string"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"run","payloadType":"str","x":110,"y":1100,"wires":[["a4fd2a69.8a67d8"]]},{"id":"37252e9b.d269e2","type":"inject","z":"f30d21db.d2c33","name":"Stop","props":[{"p":"payload","v":"stop","vt":"str"},{"p":"topic","v":"","vt":"string"}],"repeat":"","crontab":"","once":false,"onceDelay":0.1,"topic":"","payload":"stop","payloadType":"str","x":110,"y":1160,"wires":[["a4fd2a69.8a67d8"]]},{"id":"2fd2633d.471824","type":"inject","z":"f30d21db.d2c33","name":"Reset","props":[{"p":"payload","v":"reset","vt":"str"},{"p":"topic","v":"","vt":"string"}],"repeat":"","crontab":"","once":true,"onceDelay":0.1,"topic":"","payload":"reset","payloadType":"str","x":110,"y":1040,"wires":[["a4fd2a69.8a67d8"]]},{"id":"a4fd2a69.8a67d8","type":"function","z":"f30d21db.d2c33","name":"","func":"if (msg.payload == \"reset\") {\n    flow.set(\"counter\",0);\n}\n\nflow.set(\"status\",msg.payload);","outputs":0,"noerr":0,"x":310,"y":1100,"wires":[]},{"id":"17ce642d.6d27fc","type":"inject","z":"f30d21db.d2c33","name":"","props":[{"p":"payload","v":"1","vt":"num"},{"p":"topic","v":"","vt":"string"}],"repeat":"1","crontab":"","once":true,"onceDelay":"0.5","topic":"","payload":"1","payloadType":"num","x":110,"y":1220,"wires":[["4cb2b4e8.78bd5c"]]},{"id":"4cb2b4e8.78bd5c","type":"function","z":"f30d21db.d2c33","name":"","func":"var status = flow.get(\"status\")  || \"stop\";\nvar count  = flow.get(\"counter\") || 0;\n\nif (status == \"run\"){\n    count = count + 1;\n}\n\nflow.set(\"counter\",count);\nmsg.payload = count;\nreturn msg;\n","outputs":1,"noerr":0,"x":310,"y":1220,"wires":[["8e0b9b73.e5c24"]]},{"id":"7aff8596.4efb54","type":"debug","z":"f30d21db.d2c33","name":"","active":false,"tosidebar":true,"console":false,"tostatus":false,"complete":"false","x":630,"y":1220,"wires":[]},{"id":"8e0b9b73.e5c24","type":"rbe","z":"f30d21db.d2c33","name":"","func":"rbe","gap":"","start":"","inout":"out","property":"payload","x":470,"y":1220,"wires":[["7aff8596.4efb54"]]}]
```

# IBMCloud and NPM Commands

### Manage "node" and "npm" Version in IBMCloud
In the package.json can specify the version or add npm gestor
```
"engines": {
  "node": "6.9.x",
  "npm": "2.15.x"
}
```

- Reference: 
  - https://docs.cloudfoundry.org/buildpacks/node/index.html#vendoring
  - https://github.com/IBM-Cloud/node-helloworld
  - https://stackoverflow.com/questions/58384179/syntaxerror-cannot-use-import-statement-outside-a-module
  
### Install a package with enviroment variables 

#### Installing Twilio
First configure the enviroment variables:
- TWILIO_ACCOUNT_SID
- TWILIO_AUTH_TOKEN

Add ```"twilio-node": "^3.54.1"``` to package.json

- Reference: https://www.npmjs.com/package/twilio

### Upgrade "npm"
```
npm install -g npm
```

### See the version 
```bash
npm info <PACKAGE-NAME> version
```

### See the global package installed
```
npm list -g --depth 0
```

### Install package
- local packages are installed in the directory where you run ```npm install <package-name>@<version>```, and they are put in the node_modules folder under this directory
- global packages are all put in a single place in your system (exactly where depends on your setup), regardless of where you run ```npm install -g <package-name>@<version>```

### See information of lastest package
```bash
npm view <PACKAGE-VERSION>@latest
```

### See problems with packages 
Print in console the problems with errors and dependencies to install.
```bash
npm audit fix
```

### Clear cache
```
npm cache clear --force
```

### Path to Node-red

#### Windows 
```
C:\Users\<USER>\.node-red\node_modules
```


## More Information
- http://linkedbuildingdata.net/ldac2019/summerschool/files/05_Terkaj_Node_Red_Tutorial_Lecture.pdf
- https://blog.josequinto.com/2017/06/23/npm-install-fails-on-windows-10-enoent-4058-operation-not-permitted-rename/#Environment
