# PayPal Pay

* I have successfully implemented Paypal Payment Gateway using WebView. I have used some of Paypal’s available APIs for Payment which are officially available for integration in websites.

Just add this git package in your pubspec.yaml
Like :
```
paypal_pay:  
    git: https://github.com/jadejadivyaraj4/paypal_pay.git
```

Then just need to navigate to package class on the pay button and click
Like:
```dart
Navigator.of(context).push(
  MaterialPageRoute(
    builder: (BuildContext context) => UsePaypal(
        clientId: StringUtils.clientId,
        secretKey: StringUtils.secretKey,
        returnURL: "https://samplesite.com/return",
        cancelURL: "https://samplesite.com/cancel",
        transactions: [value],
        note: StringUtils.paypalNote,
        onSuccess: (Map params) async {
          print("onSuccess: $params");
          showSuccessToast("Payment Success.");
        },
        onError: (error) {
          print("onError: $error");
          showErrorToast("Payment Failed.");
        },
        onCancel: (params) {
          print('cancelled: $params');
          showErrorToast("Something Wrong.");
        }),
  ),
)
```
If you are using the Get package use the below code for navigating

```
Get.to(UsePaypal(
        clientId: StringUtils.clientId,
        secretKey: StringUtils.secretKey,
        returnURL: "https://samplesite.com/return",
        cancelURL: "https://samplesite.com/cancel",
        transactions: [value],
        note: StringUtils.paypalNote,
        onSuccess: (Map params) async {
          print("onSuccess: $params");
          showSuccessToast("Payment Success.");
        },
        onError: (error) {
          print("onError: $error");
          showErrorToast("Payment Failed.");
        },
        onCancel: (params) {
          print('cancelled: $params');
          showErrorToast("Something Wrong.");
        }),
  ));
  ```

Here you can get `clientId` and `secretKey` from [paypal developer console](https://developer.paypal.com/) that is unique keys for your project.

Note : If you don't have Paypal account yet, then create a new from this link [paypal account creation](https://developer.paypal.com/developer/accounts/create)

ReturnUrl & CancelUrl is required because we get payment using web view and that redirect success or failed that particular URL.

Transactions values are map of our item details

Like :
```dart
Map<dynamic, dynamic> value = {
  "amount": {
    "total": '10.12',
    "currency": "USD",
    "details": {"subtotal": '10.12', "shipping": '0', "shipping_discount": 0}
  },
  "description": "The payment transaction description.",
  "item_list": {
    "items": [
      {"name": "MacBook Air", "quantity": 1, "price": '10.12', "currency": "USD"}
    ],

    // shipping address is not required though
    "shipping_address": {"recipient_name": "Dev", "line1": "Travis County", "line2": "", "city": "Austin", "country_code": "US", "postal_code": "73301", "phone": "+00000000", "state": "Texas"},
  }
};
```


