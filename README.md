# FastPay Merchant SDK (iOS).  [![Generic badge](https://img.shields.io/badge/Swift-5-FA7343?style=for-the-badge&logo=swift&logoColor=white)](https://shields.io/) [![Generic badge](https://img.shields.io/badge/Xcode-13.0-007ACC?style=flat-square&logo=Xcode&logoColor=white)](https://shields.io/)



[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)]()
[![Website shields.io](https://img.shields.io/website-up-down-green-red/http/shields.io.svg)](https://fastpay.blackace.tech)
[![PyPI license](https://img.shields.io/pypi/l/ansicolortags.svg)](https://pypi.python.org/pypi/ansicolortags/)
[![Generic badge](https://img.shields.io/badge/Version-v1.0.0-blue.svg)](https://shields.io/)

This is official documentation for fastpay merchant SDK.

![alt text](https://fastpay.blackace.tech/images/logo_dark.png)


## Scaffolding Provided
This repository provides the following components that are common to our open source projects:

- FastpaySDK.framework
- FastPaySDKDocumentation.pdf



## 1.Get Started
						
Drag and drop the framework file in your project. Check ‘Copy items if needed’ and select your target.

After successfully adding the framework file in your project, select project file from Xcode’s Project Navigator and follow the selections below:

#### Target → General → Framework, Libraries and Embedded Content
and then select ​**Embed & Sign**​ for the added framework as shown below


## 2. Implementation

Import FastpayMerchantSDK in your class
```swift
import FastpayMerchantSDK
```
		

Make your class conform to FastPayDelegate delegate
```swift
class ViewController: UIViewController, FastPayDelegate {
```

Initialize the instance of FastPay
```swift
let testObj = Fastpay(storeId: "*****", storePassword: "****", orderId: "*****", amount: 500, currency: .IQD)
```
 
Set your class as delegate for FastPayDelegate
```swift
testObj.delegate = self
```
 
Start your work with that. Use .Production for production release and use .SandBox for development test.
```swift
testObj.start(in: self, for: .Production)
```

#### Parameters to pass when initiating	
```
start(in: ….)  → your view controller class that you want the SDK to present on
storeId → Merchant’s provided store ID.
storePassword → Merchant’s provided store password.
orderId → Merchant’s provided order ID.
amount → Payable amount in the transaction.
currency → In which currency order will  perform.		
```

```swift
 Fastpay(storeId: "*****", storePassword: "****", orderId: "*****", amount: 500, currency: .IQD)
```

Implement FastPaySDK delegate method to get transaction result

For Success Case
```swift
func fastpayTransactionSucceeded(with transaction: FPTransaction) {}
```

You will get the following data from transaction object in the delegate function

```swift
 transactionId: String?
 orderId: String?
 amount: Int?
 currency: FPCurrency?
 customerMobileNo: String?
 customerName: String?
 status: String?
 transactionTime: String?
 ```

## Sample Test Code
```swift
class ViewController: UIViewController, FastPayDelegate {
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
    }

    @IBAction func showAction(_ sender: UIButton){
        callSDK()
    }
    
    func callSDK(){
        let testObj = Fastpay(storeId: "1953_693", storePassword: "Password100@", orderId: "order240", amount: 500, currency: .IQD)
        testObj.delegate = self
        testObj.start(in: self, for: .Sandbox)
    }
    
    func fastpayTransactionSucceeded(with transaction: FPTransaction) {

        if let transactionId = transaction.transactionId, let orderID = transaction.orderId, let billAmount = transaction.amount, let currency = transaction.currency, let customerMobileNo = transaction.customerMobileNo, let name = transaction.customerName, let status = transaction.status, let transactionTime = transaction.transactionTime{
            print("Transaction ID : \(transactionId)")
            print("Order ID : \(orderID)")
            print("Amount : \(orderID)")
            print("Bill Amount : \(billAmount)")
            print("Currency : \(currency)")
            print("Mobile Number : \(customerMobileNo)")
            print("Name : \(name)")
            print("Status : \(status)")
            print("Transaction Time : \(transactionTime)")
        }
    }
    
    func fastpayTransactionFailed(with orderId: String) {
        print("Failed Order ID: \(orderId)")
    }
}
 ```
 
#### For details or clearification you can get help from document pdf. 
