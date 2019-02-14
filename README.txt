# blockchain-training-labs

Jonathan Pio Balane
Blockchain Cadet

Requirement Software Applications:
	- Virtual Machine
	- Ubuntu OS img(if using Virtual Machine)
	- Postman
	- Visual Studio Code(to see the codes of this repository)

NOTE: If you already have the requirement softwares proceed to the cloning of the repository. 

To Download Virtual Machine go to this url:
	https://www.virtualbox.org/wiki/Downloads

To Download Ubuntu OS img. go to this url:
	https://www.osboxes.org/ubuntu/

After your Virtual Machine has been setup with the Ubuntu OS in it, open it and proceed to the next instruction.

If you don't have Hyperledger Fabric pre-requisites, follow this instructions:

Step 1: curl -O https://hyperledger.github.io/composer/latest/prereqs-ubuntu.sh
Step 2: chmod u+x prereqs-ubuntu.sh
Step 3: ./prereqs-ubuntu.sh

Next, download the GO Language for Linux in this url:
	https://golang.org/dl/

Step 1: Go to the directory where the file located.
Step 2: Right click inside the folder and Open the Terminal.
Step 3: Type "tar -C /user/local -xzf go1.11.5.linux-amd64.tar.gz"

Now, add Go environment variable by typing commands in your Terminal:

Step 1: export PATH=$PATH:/usr/local/go/bin
Step 2: export GOPATH=$HOME/go
Step 3: export PATH=$PATH:$GOPATH/bin

After downloading the requirements and setup, we will proceed to cloning the requirements for repository.

Open the Terminal and Create your folder for the repository and download Fabric samples, Images and Binaries by typing this command:

Step 1: mkdir 2-14-19 && cd 2-14-19
Step 2: curl -sSL http://bit.ly/2ysbOFE | bash -s -- 1.4.0

The image above is when you done downloading fabric-samples, images and binaries.

NOTE: It takes time to download the images, depends on your internet connection you have.

After you download the Fabric samples, Images and Binaries, next is Clone or download the github repository by typing this command:

Step 3: git clone https://github.com/khrandm/blockchain-training-labs
Step 4: cd fabric-samples

The image above is when you done the instructions above.


Step 5: In blockchain-training-labs folder, Copy the chaincode and supply
            folder and Paste it in fabric-samples folder you just clone.
	 Click "Merge" if already exist.

Back on the Terminal.

Step 6: cd supply

Download the required library for our chaincode by typing this commands:
NOTE: Go language must be installed(if you don't go back to page 1 and download the Go language.)

Step 7: go get github.com/golang/protobuf/proto
Step 8: go get github.com/hyperledger/fabric/common/attrmgr
Step 9: go get github.com/pkg/errors
Step 10: go get github.com/hyperledger/fabric/core/chaincode/lib/cid

Now open file manager and go to Home/go/src/github.com and copy the three folders: hyperledger, pkg, and golang. and paste it to fabric-samples/chaincode.

Next is Start Fabric by typing this command:

Step 11: ./startFabric.sh
Step 12: npm install

NOTE: If get stuck in this node-pre-gyp WARN Using request for node-pre-gyp https download just Ctrl + C.

Step 13:  node enrollAdmin.js
Step 14:  node registerSupplier.js
Step 15:  node registerOEM.js
Step 16: node registerBank.js	
Step 17: node app.js

Next, go to your Postman

NOTE: If you don't have postman, to download; type in the terminal snap install  postman.

Step 18: Select GET then type the url "localhost:3000/"
Step 19: Click SEND button.

Next is raise an invoice.

Step 20: Select POST  then type the url "localhost:3000/invoice/"
Step 21: Select the Headers Tab
Step 22: Under the Content Type key, add the key "user"
Step 23: Add the value "supplier"
Step 24: Select the Body Tab.
Step 25: Select the x-www-form-url-encoded
Step 26: Type these keys and values.
 
	invoicenumber:INVOICE001
	billedto:OEM
	invoicedate:02/08/19
	invoiceamount:10000
	itemdescription:KEYBOARD
	goodreceived:False
	ispaid:False
	paidamount:0
	repaid:False
	repaymentamount:0

Step 27: Click the Send button.

You should see  "result": "success" in Response.
Now you successfully raise an invoice.

To see your invoice follow the steps under:

Step 1: Select GET  then type the url "localhost:3000/"
Step 2: Select Headers Tab
Step 3: Under the Content Type key, add the key "user"
Step 4: Add the value "supplier"
Step 5: Click the Send button.

Next is Declare goodreceived

Step 28: Click the "+" sign.
Step 29: Select PUT then type the url "localhost:3000/invoice"
Step 30: Select Headers Tab.
Step 31: Add the key "user"
Step 32: Add the value "oem"
Step 33: Select the Body Tab
Step 34:  Select the x-www-form-url-encoded
Step 35: Type these keys and values.
 
	invoicenumber:INVOICE001
	goodreceived:OEM

Step 36: Click the Send button.

You should see  "result": "success" in Response.

Next is Bank will pay the supplier

Step 37: Click the "+" sign.
Step 38: Select PUT then type the url "localhost:3000/invoice"
Step 39: Select Headers Tab.
Step 40: Add the key "user"
Step 41: Add the value "bank"
Step 42: Select the Body Tab
Step 43:  Select the x-www-form-url-encoded
Step 44: Type these keys and values.

	invoicenumber:INVOICE001
	paidamount:9000

Step 45: Click the Send button.

You should see  "result": "success" in Response.

To check the data if updated:

Step 1: Select GET  then type the url "localhost:3000/"
Step 2: Click the Send button.

The invoice will indicate that the isPaid = true
and the paidamount will be 9000 

Next is OEM will pay the bank

Step 45: Click the "+" sign.
Step 46: Select PUT then type the url "localhost:3000/invoice"
Step 47: Select Headers Tab.
Step 48: Add the key "user"
Step 49: Add the value "oem"
Step 50: Select the Body Tab
Step 51: Select the x-www-form-url-encoded
Step 52: Type these keys and values.
 
	invoicenumber:INVOICE001
	repaymentamount:11000

NOTE: the repayment amount should be more than paidamount.

Step 53: Click the Send button.

You should see  "result": "success" in Response.

To check the data if updated:

Step 1: Select GET  then type the url "localhost:3000/"
Step 2: Click the Send button.

Now, let's check the invoice audit trail

Step 54: Select GET  then type the url "localhost:3000/"
Step 55: Select Headers Tab
Step 56: Under the Content Type key, add the key "user"
Step 57: Add the value "supplier"
Step 58: Select Body Tab.
Step 59: Select the x-www-form-url-encoded
Step 60: Type these keys and values.

	invoicenumber:INVOICE001

Step 61: Click the Send button.

You shoud see the respond from the server, change it from HTML to JSON to see a JSON format of the response


